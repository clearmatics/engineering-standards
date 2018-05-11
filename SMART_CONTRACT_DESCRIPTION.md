## Finite State Machines as a way to describe Smart Contract Mechanisms

Debating the way a mechanism to be implemented in a smart contract can be simplified by using Finite State Machines (FSM) as a visual language. Although being a basic concept of Computer Science it might be relevant to have this written somewhere, and by default use this as a standard way to describe how smart contracts operate.

State Machines are useful in describing a smart contract state, and its changes, mechanisms that are external to a smart contract are defined by other state machines. Meaning that each smart contract should have its own state machine description, if it depends on the execution of other smart contracts, that is considered an input or action that needs to take place.

Finite State Machines are composed of:
* Chain: Represented by a solid line rectangle (may only be necessary for larger architecture designs)
  * This shall encompass all smart contracts
* Smart Contract: Represented by a dotted/dashed line rectangle
  * This shall encompass all the possible different states and state transitions of the smart contract
* State: Represented by a circle and ID in the center
  * State of the smart contract (defined by the state of its data)
* Transition: Represented by an arrow
  * Indicate possible next states
* Actions: *Close*, *Reveal*, *Pay*, *Cancel*
  * Action (one or multiple function calls) that pushes transaction to happen
* Guards: [A > B]
  * Conditions that allow or stop action from being successful

In [Designing Secure Ethereum Smart Contracts: A Finite State Machine](https://arxiv.org/abs/1711.09327) section *3 Defining Smart Contracts as FSM* there is a good example of how to describe a blind auction smart contract as a FSM.

![Blind Auction State Machine](images/example_fsm.png "Example of Auction Finite State Machine (via 'Designing Secure Ethereum Smart Contracts: A Finite State Machine')")

This FSM is made of:
* States
  * ABB - Accepting Blind Bids (a blind bid is a unknown hashed value)
  * RB - Revealing Bids (revealing a bid is giving proof that you know what was the original value)
  * F - Finished (winner of the bid as been determined)
  * C - Cancelled (the bid as been cancelled and funds returned)
* Transitions (represented by the arrows)
* Actions (in italic)
  * Close - Closes the bidding period
  * Bid - Adds a new bid to the smart contract storage (and user deposits a stake)
  * Unbid - Removes bid and returns stake to user
  * Reveal - Participant reveals the bid value
  * Withdraw - Participants can withdraw stakes
  * Finish - Finish bid reveal period
  * Cancel ABB - Cancel Bid Acceptance
  * Cancel RB - Cancel Bid Reveal
* Guards
  * [depositStake >= 1ETH] - the stake deposited must be at least 1ETH
  * [now > creationTime + 5 days] - now must be five days after creation date or more
  * [values.length == secret.length] - don't really understand, but it illustrates that the guards should be as obvious as possible!
  * [ now >= creationTime + 10 days] - now must be ten days after creation date or more

The detail of the finite state machine is up to the author, but there is a trade off between detail and clarity of the description.

The main goal of this visual language is to be able to present mechanisms in a standardised way that can become clear to everyone, not to be an implementation of the smart contract.

---

Other goods notation standard to use on the mechanisms descriptions:
* Proof of TxA - P(TxA)
* Alice Signed TxA - S(Alice,TxA)
* Hashed value X - H(X)
