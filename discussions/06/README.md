# CSCD27 Discussion 6

Two companies A, located in Canada, and B, located in France, want to collaborate on a super secret project. Each company has its own internal network with private servers and they want to allow the other company to access them.

These two companies have hired you as a consultant to help them to enable their collaboration wile keeping their project secret. They are giving you a list of concerns and, for each concern, they are asking you to:

1. explain whether it is a valid concern by explaining them how they could be attacked or not
2. help them secure their networks by providing the best and the most straightforward solution to their concern

6.1 they are concerned that if the network is opened to the "outside", anybody could connect to their servers?

- solutions
	+ setup a firewall with IP whitelist

6.2 they are concerned that someone outside of their network might be able to eavesdrop or hijack their communication?

- BGP hijacking
- DNS poisoning
- packet sniffing (if hacker is on the route)
- solutions
	+ SSL ensures confidentiality and integrity
	+ DNSSEC ensures authenticity

6.3 they are concerned that people might suspect that the two are working on super secret project if they see the type of communication they have?
Yes. Hackers can see

- IP of hosts involved in the communication
- the services used based on ports
- solutions
	+ setup VPN between one company in A and another in B
