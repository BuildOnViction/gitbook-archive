# TRC25 Specification

### Abstract <a href="#abstract" id="abstract"></a>

The following standard allows for implementing a standard API for TRC-25 within smart contracts. This standard provides basic functionality to transfer tokens, allow tokens to be approved so they can be spent by another on-chain third party, and manage fees to prevent abuse of the feature.

### Motivation <a href="#motivation" id="motivation"></a>

A token standard that extends the TRC-21 standard to allow token holders to transfer tokens while paying gas fees using the token itself instead of the native network token. An alternative use would be to enable gas-sponsored smart contracts.

### TRC25 Specification <a href="#trc25-specification" id="trc25-specification"></a>

```
/**
 * @title TRC25 interface
 */
interface ITRC25 {
    event Transfer(address indexed from, address indexed to, uint256 amount);
    event Approval(address indexed owner, address indexed spender, uint256 amount);
    event Fee(address indexed from, address indexed to, address indexed issuer, uint256 amount);

    function decimals() external view returns (uint8);
    function totalSupply() external view returns (uint256);
    function balanceOf(address owner) external view returns (uint256);
    function allowance(address owner, address spender) external view returns (uint256);
    function issuer() external view returns (address);
    function estimateFee(uint256 value) external view returns (uint256);

    function transfer(address recipient, uint256 amount) external returns (bool);
    function approve(address spender, uint256 amount) external returns (bool);
    function transferFrom(address from, address to, uint256 amount) external returns (bool);
}
```

#### TRC25 API Specification <a href="#trc25-api-specification" id="trc25-api-specification"></a>

* `decimals`: Return the decimals of the token.

```
function decimals() external view returns (uint8);
```

* `totalSupply`: Returns the token total supply.

```
function totalSupply() external view returns (uint256);
```

* `balanceOf`: Returns the account balance of another account with address `who`.

```
function balanceOf(address owner) external view returns (uint256);
```

* `allowance`

```
function allowance(address owner, address spender) external view returns (uint256);
```

Returns the amount which `spender` is still allowed to withdraw from `owner`.

* `issuer`: Returns the address of the token issuer.

```
function issuer() external view returns (address);
```

The method returns the address of the token issuer. This is to ensure that only the issuer has the right to decide in regard to paying fees of token-holder transactions to the token contract in terms of the token itself. The method is to verify that no one else is able to change the token contract, except the issuer.

* `estimateFee`: Calculate the transaction fee in terms of the token that the transaction makers will have to pay. Transaction fee will be paid to the issuer of the TRC25 token contract.

```
function estimateFee(uint256 value) external view returns (uint256);
```

Ideally, the function will return the transaction fee based on the value (the number of tokens) that the transaction maker wants to transfer. Transaction fee for `allowance` the function will be estimated if the input parameter `value = 0`. The way fees are computed is not standardized. Token issuers can fully customize the implementation of the function.

This function will also be called by user wallets to evaluate fees the user must be paid.

* `transfer`: Transfers `_value` amount of tokens to address `_to`, and MUST fire the `Transfer` and `Fee` event.

```
function transfer(address _to, uint256 _value) public returns (bool success)
```

The function will call `estimateFee` function to compute the transaction fee. The function SHOULD throw if the message caller’s account balance does not have enough tokens to spend and to pay transaction fees. Once succeeded, the token balance of the sender should be reduced by `_value` plus the computed transaction fee, the balance of `_to` should be increasing `_value`, while the balance of the token issuer should be increased by the computed transaction fee.

* `approve`

```
function approve(address spender, uint256 value) external returns (bool);
```

Allows `_spender` to withdraw from your account multiple times, up to the `_value` amount. If this function is called again it overwrites the current allowance with `_value`. This function also calls `estimateFee` with input parameter 0 in order to compute the transaction fee in terms of tokens that the transaction sender must pay to the token issuer.

* `transferFrom`

```
function transferFrom(address from, address to, uint256 value) external returns (bool);
```

Transfers `value` amount of tokens from address `from` to address `to`. The function must fire the `Transfer` and `Fee` event.

#### TRC25 Event specification <a href="#trc25-event-specification" id="trc25-event-specification"></a>

* `Transfer`

```
event Transfer(address indexed from, address indexed to, uint256 amount);
```

This event MUST be emitted when tokens are transferred in functions `transfer` and `transferFrom`.

* `Approval`

```
event Approval(address indexed owner, address indexed spender, uint256 amount);
```

This event MUST be emitted on any successful call to `approve` function.

* `Fee`

```
event Fee(address indexed from, address indexed to, address indexed issuer, uint256 amount);
```

This event MUST be emitted when tokens are transferred in functions `transfer` and `transferFrom` in order for clients/DApp/third-party wallets to notify its users about the paid transaction fee in terms of token.

#### Implementation <a href="#implementation" id="implementation"></a>

To implement the TRC-25 standard, the following fields must be put at the beginning of the smart contract.

```
mapping (address => uint256) private _balances;
uint256 private _minFee;
address private _owner;
```

This standard will need some basic information to tracking and

* `_balances`: record the balance of each token holder
* `_minFee`: the minimum fee in terms of tokens that the transaction sender must pay. Ideally minFee will be paid when `approve` function is called or when transaction fails.
* `_owner`: the address of the token issuer who will receive transaction fees from token holders in terms of token, but will pay transaction fees to masternodes by means of TOMO.

The implementation also defines some additional functions as follows:

* `issuer`: Returns the address of the issuer of the token.
* `minFee`: Returns the minimum fee for any transaction.

```
/**
 * @title Base TRC-25 implementation
 * @notice TRC-25 implementation for opt-in to gas sponsor program. This replace Ownable from OpenZeppelin as well.
 */
contract TRC25 is ITRC25 {
    // The order of _balances, _minFeem, _issuer must not be changed to pass validation of gas sponsor application
    mapping (address => uint256) private _balances;
    uint256 private _minFee;
    address private _owner;
    address private _newOwner;

    mapping (address => mapping (address => uint256)) private _allowances;

    string private _name;
    string private _symbol;
    uint8 private _decimals;
    uint256 private _totalSupply;

    event FeeUpdated(uint256 fee);
    event OwnershipTransferred(address indexed previousOwner, address indexed newOwner);

    constructor(string memory name, string memory symbol, uint8 decimals) {
        _name = name;
        _symbol = symbol;
        _decimals = decimals;
        _owner = msg.sender;
    }

    /**
     * @dev Throws if called by any account other than the owner.
     */
    modifier onlyOwner() {
        require(_owner == msg.sender, "TRC25: caller is not the owner");
        _;
    }

    /**
     * @notice Returns the name of the token
     */
    function name() public view returns (string memory) {
        return _name;
    }

    /**
     * @notice Returns the name of the token
     */
    function symbol() public view returns (string memory) {
        return _symbol;
    }

    /**
     * @notice Returns the number of decimals used to get its user representation.
     * For example, if `decimals` equals `2`, a balance of `505` tokens should
     * be displayed to a user as `5,05` (`505 / 10 ** 2`).
     */
    function decimals() public view override returns (uint8) {
        return _decimals;
    }

    /**
     * @notice Returns the amount of tokens in existence.
     */
    function totalSupply() public view override returns (uint256) {
        return _totalSupply;
    }

    /**
     * @notice Returns the amount of tokens owned by `account`.
     * @param owner The address to query the balance of.
     * @return An uint256 representing the amount owned by the passed address.
     */
    function balanceOf(address owner) public view override returns (uint256) {
        return _balances[owner];
    }

    /**
     * @notice Returns the remaining number of tokens that `spender` will be
     * allowed to spend on behalf of `owner` through {transferFrom}. This is
     * zero by default.
     *
     * This value changes when {approve} or {transferFrom} are called.
     */
    function allowance(address owner,address spender) public view override returns (uint256){
        return _allowances[owner][spender];
    }

    /**
     * @notice Owner of the token
     */
    function owner() public view returns (address) {
        return _owner;
    }

    /**
     * @notice Owner of the token
     */
    function issuer() public view override returns (address) {
        return _owner;
    }

    /**
     * @notice Minimum amount of token should be paid in a transaction
     */
    function minFee() public view returns (uint256) {
        return _minFee;
    }

    /**
     * @notice Calculate fee required for action related to this token
     * @param value Amount of fee
     */
    function estimateFee(uint256 value) public virtual view override returns (uint256) {
        return _minFee;
    }

    /**
     * @notice Moves `amount` tokens from the caller's account to `recipient`.
     *
     * Returns a boolean value indicating whether the operation succeeded.
     *
     * Emits a {Transfer} event.
     */
    function transfer(address recipient, uint256 amount) public override returns (bool) {
        uint256 fee = estimateFee(amount);
        uint256 total = amount + fee;
        require(total >= amount, "TRC25: integer overflow");

        _transfer(msg.sender, recipient, amount);
        _transferFee(msg.sender, recipient, fee);
        return true;
    }

    /**
     * @notice Sets `amount` as the allowance of `spender` over the caller's tokens.
     *
     * Returns a boolean value indicating whether the operation succeeded.
     *
     * IMPORTANT: Beware that changing an allowance with this method brings the risk
     * that someone may use both the old and the new allowance by unfortunate
     * transaction ordering. One possible solution to mitigate this race
     * condition is to first reduce the spender's allowance to 0 and set the
     * desired value afterwards:
     * https://github.com/ethereum/EIPs/issues/20#issuecomment-263524729
     *
     * Emits an {Approval} event.
     */
    function approve(address spender, uint256 amount) public override returns (bool) {
        require(spender != address(0), "TRC25: approve to the zero address");

        _allowances[msg.sender][spender] = amount;
        emit Approval(msg.sender, spender, amount);
        _transferFee(msg.sender, address(this), _minFee);
        return true;
    }

    /**
     * @notice Moves `amount` tokens from `sender` to `recipient` using the
     * allowance mechanism. `amount` is then deducted from the caller's
     * allowance.
     *
     * Returns a boolean value indicating whether the operation succeeded.
     *
     * Emits a {Transfer} event.
     */
    function transferFrom(address sender, address recipient, uint256 amount) public override returns (bool) {
        uint256 fee = estimateFee(amount);
        uint256 total = amount + fee;
        require(total >= amount, "TRC25: integer overflow");
        require(_allowances[sender][msg.sender] >= total, "TRC25: amount exeeds allowance");

        _allowances[sender][msg.sender] = _allowances[sender][msg.sender] - total;
        _transfer(sender, recipient, amount);
        _transferFee(sender, recipient, fee);
        return true;
    }

    /**
     * @notice Issues `amount` tokens to the designated `address`.
     *
     * Can only be called by the current owner.
     */
    function mint(address recipient, uint256 amount) public onlyOwner returns (bool) {
        _mint(recipient, amount);
        return true;
    }

    /**
     * @notice Remove `amount` tokens owned by caller from circulation.
     */
    function burn(uint256 amount) public returns (bool) {
        _burn(msg.sender, amount);
        _transferFee(msg.sender, address(this), _minFee);
        return true;
    }

    /**
     * @dev Accept the ownership transfer. This is to make sure that the contract is
     * transferred to a working address
     *
     * Can only be called by the newly transfered owner.
     */
    function acceptOwnership() public {
        require(msg.sender == _newOwner, "TRC25: only new owner can accept ownership");
        address oldOwner = _owner;
        _owner = _newOwner;
        _newOwner = address(0);
        emit OwnershipTransferred(oldOwner, _owner);
    }

    /**
     * @dev Transfers ownership of the contract to a new account (`newOwner`).
     *
     * Can only be called by the current owner.
     */
    function transferOwnership(address newOwner) public onlyOwner {
        require(newOwner != address(0), "TRC25: new owner is the zero address");
        _newOwner = newOwner;
    }

    /**
     * @notice Set minimum fee for each transaction
     *
     * Can only be called by the current owner.
     */
    function setFee(uint256 fee) public onlyOwner {
        _setMinFee(fee);
    }

    /**
     * @dev Internal function that takes an amount of the token to compensate
     * for the gas user used for execute a specified function
     * @param value Amount of token to charge
     */
    function _charge(uint256 value) internal {
        _transferFee(msg.sender, address(this), value);
    }

    /**
     * @dev Transfer token for a specified addresses
     * @param from The address to transfer from.
     * @param to The address to transfer to.
     * @param amount The amount to be transferred.
     */
    function _transfer(address from, address to, uint256 amount) internal {
        require(from != address(0), "TRC25: transfer from the zero address");
        require(to != address(0), "TRC25: transfer to the zero address");
        require(amount <= _balances[from], "TRC25: insuffient balance");
        _balances[from] = _balances[from] - amount;
        _balances[to] = _balances[to] + amount;
        emit Transfer(from, to, amount);
    }

    /**
     * @dev Internal function to transfer fee for a specified transaction
     * @param from The address that is source of token transfer or address that execute the transaction
     * @param to The address that is destination of token transfer. If not token transfer should be address of contract
     * @param amount The amount token as fee
     */
    function _transferFee(address from, address to, uint256 amount) internal {
        uint256 fee = estimateFee(amount);
        if(fee > 0) {
            _transfer(from, _owner, fee);
            emit Fee(from, to, _owner, fee);
        }
    }

    /**
     * @dev Internal function that mints an amount of the token and assigns it to
     * an account. This encapsulates the modification of balances such that the
     * proper events are emitted.
     * @param to The account that will receive the created tokens.
     * @param amount The amount that will be created.
     */
    function _mint(address to, uint256 amount) internal {
        require(to != address(0), "TRC25: mint to the zero address");
        _totalSupply = _totalSupply + amount;
        _balances[to] = _balances[to] + amount;
        emit Transfer(address(0), to, amount);
    }

    /**
     * @dev Internal function that burns an amount of the token
     * This encapsulates the modification of balances such that the
     * proper events are emitted.
     * @param from The account that token amount will be deducted.
     * @param amount The amount that will be burned.
     */
    function _burn(address from, uint256 amount) internal {
        require(from != address(0), "TRC25: burn from the zero address");
        require(amount <= _balances[from], "TRC25: insuffient balance");
        _totalSupply = _totalSupply - amount;
        _balances[from] = _balances[from] - amount;
        emit Transfer(from, address(0), amount);
    }

    /**
     * @dev Internal function set minimum fee
     */
    function _setMinFee(uint256 fee) internal {
        _minFee = fee;
        emit FeeUpdated(fee);
    }
}
```

#### TRC25 Token example <a href="#trc25-token-example" id="trc25-token-example"></a>

The following example demonstrates a token using the TRC25 standard with custom fee.

```
contract MyTRC25 is TRC25 {
    string private _name;
    string private _symbol;
    uint8 private _decimals;

    constructor (string memory name, string memory symbol, uint8 decimals, uint256 minFee) TRC25(name, symbol, decimals) {
        _setMinFee(minFee);
    }

    function estimateFee(uint256 value) public view override returns (uint256) {
        uint256 fee = value / 10000;
        if(fee > minFee()) {
            return fee;
        }
        return minFee();
    }
```
