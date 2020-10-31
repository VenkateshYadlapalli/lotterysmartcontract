pragma solidity >=0.5.13 < 0.7.3;

contract Lottery{
    
    address public owner;
    mapping(address => uint) public addressoflotteryparticipants;
    address[] public  addressofparticipants;
    constructor() public {
        owner=msg.sender;
        
    }
    function receiveEtherfromParticipants() payable public{
        require(msg.value>1 ether,"You require more than one ether to participate in this lottery");
        require(contains(msg.sender)==0,"each account is allowed to participate only once");
        addressoflotteryparticipants[msg.sender]=msg.value;
        addressofparticipants.push(msg.sender);
        
    }
    function randomNumberFunction() private onlyOwner returns(uint){
        uint randomNumber= uint(keccak256(abi.encodePacked(block.difficulty,block.timestamp,msg.sender,
        addressofparticipants)))%addressofparticipants.length;
        return(randomNumber);
        
    }
    function findtheWinner() payable public  {
        uint randomnumber=randomNumberFunction();
        address payable winner=payable(addressofparticipants[randomnumber]);
        winner.transfer(address(this).balance);
        
    }
    
    modifier onlyOwner(){
        require(msg.sender==owner,"Only owner have the access");
        _;
    }
    function contains(address addr) private  returns(uint){
        return(addressoflotteryparticipants[addr]);
    }
    
}

