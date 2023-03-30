---
layout: post
title:  "Syntax highlighting"
date:   2019-11-06 01:11:00 +0100
categories:
---

# Syntax highlighting
This theme supports syntax respectively code highlighting. Below you find some examples of different programming languages.

<br />solidity:
{% highlight solidity %}
pragma solidity 0.7.5;

contract AnonymousBase {
    
    //array of founder addresses
    address[] founders;
    
    //number of founder approvals required for transfer
    uint requiredApprovals;
    
    //number of founder approvals
    uint approvals = 0;
    
    //mapping of founders already approved
    mapping (address => bool) approved;
    
    //amount to transfer
    uint transferAmount;
    
    //address to transfer
    address payable transferAddress;
    
    //logs
    event deposited(uint amount, address indexed depositedFrom);
    event transferred(uint amount, address indexed transferredTo);
    
    //require msg.sender to be a founder address
    modifier onlyFounders{
        address founder;
        uint i = 0;
        while (i < founders.length){
            if(msg.sender == founders[i]){
                founder = founders[i];
                i = founders.length;
            }
        i++;
        }
        require(msg.sender == founder, "I don't know you like that, you nobody.");
        _;
    }
    
    //add founder function
    function addFounder(address _address) internal{
        //add to founders array
        founders.push(_address);
        
        //add to approved mapping
        approved[msg.sender] = false;
    }
    
    //reset function
    function reset() internal{
        //reset transfer request
        delete transferAmount;
        delete transferAddress;
        
        //reset approvals
        approvals = 0;
        for (uint i = 0; i < founders.length; i++){
            approved[founders[i]] = false;
        }
    }
    
}
