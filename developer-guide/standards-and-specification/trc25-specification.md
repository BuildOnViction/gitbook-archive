---
description: TRC25 is the official standard for fungible tokens in TomoChain ecosystem.
---

# TRC25 Specification

### Abstract <a href="#abstract" id="abstract"></a>

The following standard allows for the implementation of a standard API for tokens within smart contracts. This standard provides basic functionality to transfer tokens, as well as allow tokens to be approved so they can be spent by another on-chain third party. This standard also defines how fee should be managed to prevent abuse of the feature.

### Motivation <a href="#motivation" id="motivation"></a>

For EVM-based blockchain, ERC20 has became the standard for fungible tokens. This standard works perfectly and had been proven for a long time. However, due to the way smart-contract works in blockchain, it's somewhat difficult for new users to understand, especially web2 users.

TRC25 is developed in effort to simplify the way a token works by eliminate the need of gas when using the token. It means that users won't need to keep native token when they transfer, approve or any other actions available on the token. Instead the fee for the network can be paid by the token itself.

### Specification <a href="#trc25-specification" id="trc25-specification"></a>

```solidity
interface IVRC25 {
    event Transfer(address indexed from, address indexed to, uint256 value);
    event Approval(address indexed owner, address indexed spender, uint256 value);
    event Fee(address indexed from, address indexed to, address indexed issuer, uint256 value);

    function decimals() external view returns (uint8);
    function totalSupply() external view returns (uint256);
    function balanceOf(address owner) external view returns (uint256);
    function issuer() external view returns (address);
    function allowance(address owner, address spender) external view returns (uint256);
    function estimateFee(uint256 value) external view returns (uint256);
    function transfer(address recipient, uint256 value) external returns (bool);
    function approve(address spender, uint256 value) external returns (bool);
    function transferFrom(address from, address to, uint256 value) external  returns (bool);
}
```

Source: [IVRC25.sol](https://github.com/tomochain/trc25/blob/main/contracts/interfaces/IVRC25.sol)

#### Methods <a href="#trc25-api-specification" id="trc25-api-specification"></a>

* `decimals`: Return the decimals of the token.

```solidity
function decimals() external view returns (uint8);
```

* `totalSupply`: Returns the token total supply.

```solidity
function totalSupply() external view returns (uint256);
```

* `balanceOf`: Returns the account balance of another account with address `owner`.

```solidity
function balanceOf(address owner) external view returns (uint256);
```

* `allowance`

```solidity
function allowance(address owner, address spender) external view returns (uint256);
```

Returns the amount which `spender` is still allowed to withdraw from `owner`.

* `issuer`: Returns the address of the token issuer.

```solidity
function issuer() external view returns (address);
```

The method returns the address of the token issuer. This is to ensure that only the issuer has the right to decide in regard to paying fees of token-holder transactions to the token contract in terms of the token itself. The method is to verify that no one else is able to change the token contract, except the issuer.

* `estimateFee`: Calculate the transaction fee in terms of the token that the transaction makers will have to pay. Transaction fee will be paid to the issuer of the TRC25 token contract.

```solidity
function estimateFee(uint256 value) external view returns (uint256);
```

Ideally, the function will return the transaction fee based on the value (the number of tokens) that the transaction maker wants to transfer. Transaction fee for `allowance` the function will be estimated if the input parameter `value = 0`. The way fees are computed is not standardized. Token issuers can fully customize the implementation of the function.

This function will also be called by user wallets to evaluate fees the user must pay.

* `transfer`: Transfers `value` amount of tokens to address `recipient`, and MUST fire the `Transfer` and `Fee` event.

```solidity
function transfer(address recipient, uint256 value) public returns (bool success)
```

The function will call `estimateFee` function to compute the transaction fee. The function SHOULD throw if the message caller’s account balance does not have enough tokens to spend and to pay transaction fees. Once succeeded, the token balance of the sender should be reduced by `value` plus the computed transaction fee, the balance of `recipient` should be increasing `value`, while the balance of the token issuer should be increased by the computed transaction fee.

* `approve`

```solidity
function approve(address spender, uint256 value) external returns (bool);
```

Allows `spender` to withdraw from your account multiple times, up to the `value` amount. If this function is called again it overwrites the current allowance with `value`. This function also calls `estimateFee` with input parameter 0 in order to compute the transaction fee in terms of tokens that the transaction sender must pay to the token issuer.

* `transferFrom`

```solidity
function transferFrom(address from, address to, uint256 value) external returns (bool);
```

Transfers `value` amount of tokens from the address `from` to the address `to`. The function must fire the `Transfer` and `Fee` events.

#### Events <a href="#trc25-event-specification" id="trc25-event-specification"></a>

* `Transfer`

```solidity
event Transfer(address indexed from, address indexed to, uint256 amount);
```

This event MUST be emitted when tokens are transferred in functions `transfer` and `transferFrom`.

* `Approval`

```solidity
event Approval(address indexed owner, address indexed spender, uint256 amount);
```

This event MUST be emitted on any successful call to `approve` function.

* `Fee`

```solidity
event Fee(address indexed from, address indexed to, address indexed issuer, uint256 amount);
```

This event MUST be emitted when tokens are transferred in functions `transfer` and `transferFrom` in order for clients/DApp/third-party wallets to notify their users about the paid transaction fee in terms of tokens.

### Requirement <a href="#implementation" id="implementation"></a>

For a contract to meet TRC25 requirements, it must satisfy the following conditions:

* Implement `IVRC25` interface in the specification.
* Have 3 first storage slots in the contracts as follow:&#x20;

```solidity
mapping (address => uint256) private _balances;
uint256 private _minFee;
address private _owner;
```

* Implement `Permit` extension, as defined in EIP-2612. Permit acts as a fallback for any gas-less protocol to support your token properly, in the case that your token isn't registered for [TomoZ](../integration/tomoz-integration.md).

```solidity
interface IVRC25Permit {
    function nonces(address owner) external view returns (uint256);
    function permit(address owner, address spender, uint256 value, uint256 deadline, uint8 v, bytes32 r, bytes32 s) external;
}
```

### Implementation <a href="#implementation" id="implementation"></a>

To implement the TRC25 standard, the following fields must be put at the beginning of the smart contract.

```solidity
mapping (address => uint256) private _balances;
uint256 private _minFee;
address private _owner;
```

This standard will need some basic information to track and

* `_balances`: record the balance of each token holder
* `_minFee`: the minimum fee in terms of tokens that the transaction sender must pay. Ideally, minFee will be paid when the `approve` function is called or when the transaction fails.
* `_owner`: the address of the token issuer who will receive transaction fees from token holders in terms of the token, but will pay transaction fees to masternodes by means of TOMO.

The implementation also defines some additional functions as follows:

* `issuer`: Returns the address of the issuer of the token.
* `minFee`: Returns the minimum fee for any transaction.

```solidity
/**
 * @title Base VRC25 implementation
 * @notice VRC25 implementation for opt-in to gas sponsor program. This replace Ownable from OpenZeppelin as well.
 */
abstract contract VRC25 is IVRC25, IERC165 {
    using Address for address;
    using SafeMath for uint256;

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

    constructor(string memory name, string memory symbol, uint8 decimals_) internal {
        _name = name;
        _symbol = symbol;
        _decimals = decimals_;
        _owner = msg.sender;
    }

    /**
     * @dev Throws if called by any account other than the owner.
     */
    modifier onlyOwner() {
        require(_owner == msg.sender, "VRC25: caller is not the owner");
        _;
    }

    /**
     * @notice Name of token
     */
    function name() public view returns (string memory) {
        return _name;
    }

    /**
     * @notice Symbol of token
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
     * @dev The amount fee that will be lost when transferring.
     */
    function minFee() public view returns (uint256) {
        return _minFee;
    }

    /**
     * @notice Calculate fee needed to transfer `amount` of tokens.
     */
    function estimateFee(uint256 value) public view override returns (uint256) {
        if (address(msg.sender).isContract()) {
            return 0;
        } else {
            return _estimateFee(value);
        }
    }

    /**
     * @notice Moves `amount` tokens from the caller's account to `recipient`.
     *
     * Returns a boolean value indicating whether the operation succeeded.
     *
     * Emits a {Transfer} event.
     */
    function transfer(address recipient, uint256 amount) external override returns (bool) {
        uint256 fee = estimateFee(amount);
        _transfer(msg.sender, recipient, amount);
        _chargeFeeFrom(msg.sender, recipient, fee);
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
    function approve(address spender, uint256 amount) external override returns (bool) {
        uint256 fee = estimateFee(0);
        _approve(msg.sender, spender, amount);
        _chargeFeeFrom(msg.sender, address(this), fee);
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
    function transferFrom(address sender, address recipient, uint256 amount) external override returns (bool) {
        uint256 fee = estimateFee(amount);
        require(_allowances[sender][msg.sender] >= amount.add(fee), "VRC25: amount exeeds allowance");

        _allowances[sender][msg.sender] = _allowances[sender][msg.sender].sub(amount).sub(fee);
        _transfer(sender, recipient, amount);
        _chargeFeeFrom(sender, recipient, fee);
        return true;
    }

    /**
     * @notice Remove `amount` tokens owned by caller from circulation.
     */
    function burn(uint256 amount) external returns (bool) {
        uint256 fee = estimateFee(0);
        _burn(msg.sender, amount);
        _chargeFeeFrom(msg.sender, address(this), fee);
        return true;
    }

    /**
     * @dev Accept the ownership transfer. This is to make sure that the contract is
     * transferred to a working address
     *
     * Can only be called by the newly transfered owner.
     */
    function acceptOwnership() external {
        require(msg.sender == _newOwner, "VRC25: only new owner can accept ownership");
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
    function transferOwnership(address newOwner) external virtual onlyOwner {
        require(newOwner != address(0), "VRC25: new owner is the zero address");
        _newOwner = newOwner;
    }

    /**
     * @notice Set minimum fee for each transaction
     *
     * Can only be called by the current owner.
     */
    function setFee(uint256 fee) external virtual onlyOwner {
        _minFee = fee;
        emit FeeUpdated(fee);
    }

    /**
     * @dev Returns true if this contract implements the interface defined by
     * `interfaceId`. See the corresponding
     * https://eips.ethereum.org/EIPS/eip-165#how-interfaces-are-identified[EIP section]
     * to learn more about how these ids are created.
     *
     */
    function supportsInterface(bytes4 interfaceId) public view override virtual returns (bool) {
        return interfaceId == type(IVRC25).interfaceId;
    }

    /**
     * @notice Calculate fee needed to transfer `amount` of tokens.
     */
    function _estimateFee(uint256 value) internal view virtual returns (uint256);

    /**
     * @dev Transfer token for a specified addresses
     * @param from The address to transfer from.
     * @param to The address to transfer to.
     * @param amount The amount to be transferred.
     */
    function _transfer(address from, address to, uint256 amount) internal {
        require(from != address(0), "VRC25: transfer from the zero address");
        require(to != address(0), "VRC25: transfer to the zero address");
        require(amount <= _balances[from], "VRC25: insuffient balance");
        _balances[from] = _balances[from].sub(amount);
        _balances[to] = _balances[to].add(amount);
        emit Transfer(from, to, amount);
    }

    /**
     * @dev Set allowance that spender can use from owner
     * @param owner The address that authroize the allowance
     * @param spender The address that can spend the allowance
     * @param amount The amount that can be allowed
     */
    function _approve(address owner, address spender, uint256 amount) internal {
        require(owner != address(0), "VRC25: approve from the zero address");
        require(spender != address(0), "VRC25: approve to the zero address");

        _allowances[owner][spender] = amount;
        emit Approval(owner, spender, amount);
    }

    /**
     * @dev Internal function to charge fee for gas sponsor function. Won't charge fee if caller is smart-contract because they are not sponsored gas.
     * NOTICE: this function is only a helper to transfer fee from an address different that msg.sender. Other validation should be handled outside of this function if necessary.
     * @param sender The address that will pay the fee
     * @param recipient The address that is destination of token transfer. If not token transfer should be address of contract
     * @param amount The amount token as fee
     */
    function _chargeFeeFrom(address sender, address recipient, uint256 amount) internal {
        if (address(msg.sender).isContract()) {
            return;
        }
        if(amount > 0) {
            _transfer(sender, _owner, amount);
            emit Fee(sender, recipient, _owner, amount);
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
        require(to != address(0), "VRC25: mint to the zero address");
        _totalSupply = _totalSupply.add(amount);
        _balances[to] = _balances[to].add(amount);
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
        require(from != address(0), "VRC25: burn from the zero address");
        require(amount <= _balances[from], "VRC25: insuffient balance");
        _totalSupply = _totalSupply.sub(amount);
        _balances[from] = _balances[from].sub(amount);
        emit Transfer(from, address(0), amount);
    }
}
```

Source: [VRC25.sol](https://github.com/tomochain/trc25/blob/main/contracts/VRC25.sol)

### Example <a href="#trc25-token-example" id="trc25-token-example"></a>

The following example demonstrates a token using the TRC25 standard with a custom fee.

The easiest way to implement TRC25 specification is to let first inheritance of your contract to be `VRC25` or `VRC25Permit`.

```solidity
contract SampleVRC25 is VRC25Permit {
    using Address for address;
    event Hello(address sender);

    constructor() public VRC25("Example Fungible Token", "EFT", 0) EIP712("VRC25Permit", "1") {
    }

    /**
     * @notice Calculate fee required for action related to this token
     * @param value Amount of fee
     */
    function _estimateFee(uint256 value) internal view override returns (uint256) {
        return value + minFee();
    }

    function sayHello() public {
        _chargeFeeFrom(msg.sender, address(0), estimateFee(0));

        emit Hello(msg.sender);
    }

    function supportsInterface(bytes4 interfaceId) public view override returns (bool) {
        return interfaceId == type(IVRC25).interfaceId || super.supportsInterface(interfaceId);
    }

    /**
     * @notice Issues `amount` tokens to the designated `address`.
     *
     * Can only be called by the current owner.
     */
    function mint(address recipient, uint256 amount) external onlyOwner returns (bool) {
        _mint(recipient, amount);
        return true;
    }
}
```

Source: [SampleVRC25.sol](https://github.com/tomochain/trc25/blob/main/contracts/tests/SampleVRC25.sol)

### Enable gas-less transaction

Once you have deployed a TRC25 compatible contract. You will also need to register for TomoZ to enable gas-less transaction for your contract. Please refer to [TomoZ](../integration/tomoz-integration.md) page for more information.
