
---
## Chapter 1
### Common ways to handle enterprise complexity

- PERFORMING MINDLESS MANUAL TESTING :(
- AVOIDING BIG CODE CHANGES :(
- DELEGATING TO AN AUTOMATED TESTING FRAMEWORK

## Chapter 2 - Groovy
As you can see in this listing,
- Classes are public by default.
- Fields are private by default.

the meaning of def is “I won’t declare a type here; please do it automatically for me.”
\

### Expando() 

Что-то похожее на моки, только быстрее для частных случаев
`
```Groovy
def "Testing invalid and valid address detection"() { 
			when: "two different addresses are checked" 
			Address invalidAddress = new Address(country:"Greece",number:23) 
			Address validAddress = new Address(country:"Greece", number:23,street:"Argous", postCode:"4534") 
			
			def dummyAddressDao = new Expando() 
			dummyAddressDao.load = { id -> return 
			id==2?validAddress:invalidAddress} 
			
			Stamper stamper = new Stamper(dummyAddressDao as AddressDao) 
			
			then: "Only the address with street and postcode is accepted"
			!stamper.isValid(1) stamper.isValid(2) }
```

