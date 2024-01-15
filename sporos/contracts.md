contracts are programmatic agreements between [[citizen]]s of [[sporos]].
they augment the nature of the [[collective-system]] by programmatically altering the [[autonomous-state]].
contracts have a specific goal that must be achieved before an expiry date, the contract should also include the conditions of success and failure for the specified goal.

for example a contract to exchange food goods might look like:

```python
contract.goal = transfer_10kg_potatoe_from_cid123_to_cid321() # Citizen 123 to transfer 10kg of potatoes to citizen 321

contract.expiry_date = "2 months"

if (contract.success):
	transfer_5_tokens_from_cid321_to_cid123() # citizen 321 pays citizen 123 for the potatoes
else:
	None

contract.activate()
```

the logic of functions is written as code that runs on the [[collective-system]] which in turns uses the [[autonomous-state]] to register whether the goal state has been achieved at the time of expiry or not.

contracts can be long lived through the use of reviews, which renew the contract at specified intervals or trigger a review of the contract if the goal wasn't met.

for example a long standing contract that states that all citizens are entitled to one [[hexagon]] might look like:

```python
contract.goal = each_citizen_has_one_hexagon()

contract.expiry = "3 months"

if (contract.success):
	contract.renew()
else:
	contract.review()

contract.activate()	
```

contracts that run on the [[collective-system]] can only affect a specific range or parameters defined by the [[autonomous-state]]. contracts that run on the [[autonomous-state]] have to be reviewed by all and voted on using [[distributed-direct-democracy]].