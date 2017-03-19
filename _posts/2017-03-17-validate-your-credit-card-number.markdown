---
layout: post
title:  "How to Validate Your Credit Card Number in Swift"
date:   2017-03-17 16:16:01 -0600
categories: jekyll update
---

Not long ago, I started CS50. For someone who hasn't done any computer science courses, it seems very interesting.

I was doing one of the exercises today asking you to write an algorithm to validate a credit card number in C. It's very useful to our daily life so I think I might be a good idea to convert it to Swift for my own reference. 

~~~ swift
func verifyCreditCardNumber(input: Int) {
    
    var myInput = input
    
    var remainder = 0, count = 0, resultMultipliedByTwo = 0, resultOfProductDigits = 0, remainderDigit = 0, sumOfDigitsNotMultipliedByTwo = 0, firstTwoDigit = 0
    
    while myInput > 0 {
        
        count += 1
        
        remainder = myInput % 10
        
        if count % 2 == 0 {
            resultMultipliedByTwo = remainder * 2
            
            while resultMultipliedByTwo > 0 {
                remainderDigit = resultMultipliedByTwo % 10
                resultOfProductDigits += remainderDigit
                resultMultipliedByTwo /= 10
            }
        } else {
            sumOfDigitsNotMultipliedByTwo += remainder
        }
        
        myInput /= 10
        
        if myInput > 10 {
            firstTwoDigit = myInput
        }
    }
    
    if (resultOfProductDigits + sumOfDigitsNotMultipliedByTwo) % 10 == 0 {
        switch firstTwoDigit {
        case 34, 37:
            print("AMEX")
        case 51...55:
            print("MASTERCARD")
        case 40...49:
            print("VISA")
        default:
            print("INVALID")
        }
    } else {
        print("INVALID")
    }
    
}
~~~