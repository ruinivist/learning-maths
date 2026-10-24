# Screwy Pirates

5 pirates and 100 gold coins. There is a seniority order of voting among them ( each distinct ). Starting from most senior, repeat

- senior proposes a plan, if excepted by atlest half, we distribute per the plan
- else senior is killed and process continues

## Solution

The key idea is to start from simples cases of 1, 2, 3... pirates and so on.

1 can just take all.
2 can also just take all.

Things become more interesting for the 3 case.

Say 3 decides (100, 0, 0), this'll definitely get him killed. I need to buy the vote of the lowest ranked case.

Consider the two case, it is guaranteed in 2 case pirate 0 gets nothing, so I offer him 1 and buy his vote.
(99, 0, 1) is the optimal allocation here.

_Adding the 4th pirate_

I too must buy votes, if my plan is voted down, allocation will be (100, 0, 1). I need 1 more voter so I try to buy the first pirate again with
(99, 0, 0, 1).

_Adding a 5th pirate_

Now the number of additional votes needed is 2. I can similarly buy the junior 2 votes.
(98, 0, 0, 1, 1)
