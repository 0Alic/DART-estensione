# :dart: L2DART: A Layer-2 DecentrAlized Role-based Trust management

L2DART is an Ethereum and Python implementation of the Role-based Trust management (RT) framework, restricted to the sub-language RT0, designed as a layer-2 system, in particular the off-chain computation approach. This is an extension of a previous work, called DART, available here: https://github.com/0Alic/DART. 

Differently from DART, where a RT policy is stored and evaluated with a smart contract, in L2DARt the approach has the following approach:
- Like in DART, users store RT credentials in a smart contract;
- The credentials are processed with the backward-search discovering algorithm off-chain, which is implemented as a Python module. The alogorithm takes in input a role and finds all the users, principals, having that role according to the credentials stored in the smart contract. Along with the result, the algorithm returns, for each principal, a proof that can be verified on-chain to check whether the result is correct or not;
- The proof can be verified by the smart contract. This is useful if we assume the off-chain Python module as untrusted.

This approach is suitable to implement role-based access control systems to protect smart contracts, in particular when the roles are assigned by multiple organizations and when a role can be assigned as a result of a combination of other roles following the RT grammar.

Moreover, verifying the proof on-chain has a striclty lower cost than executing backward-search discovering algorithm on-chain while keeping the auditability, transparency and immutability, property of blockchain and  keeping the system decentralized.

## Structure of the repository

This is a Truffle project. The DART smart contract is in `contracts/DART.sol`. The `DART.py` implements the off-chain module, i.e. the backward search algorithm improved to return the proof as well.

### Tests

* `test_epapers.py`: test scenario A;
* `test_wot_passive.py`: test scenario B, passive trust network;
* `test_wot_active.py`: test scenario B, active trust network;

Run [Ganache](https://github.com/trufflesuite/ganache) or [ganache-cli](https://github.com/trufflesuite/ganache-cli) with gas limit equal to, `12000000`, network id `1`, and 100 accounts. With ganache-cli execute `ganache-cli -l 12000000 -i 1 -a 100`. Deploy the contracts with `truffle migrate --network ganache`. Execute the test with `python3 XXX_test.py [...]`. NOTE: migrate again between tests.

## Contributors

The project has been developed by [lucaceschi](https://github.com/lucaceschi), with the support of [andreadesalve](https://github.com/andreadesalve) and [0Alic](https://github.com/0Alic).

## References

RT framework papers: [Design of a role-based trust-management framework](https://ieeexplore.ieee.org/abstract/document/1004366?casa_token=R_H0efcz51oAAAAA:ZVyPlVbJcMcT8HSW8_A_Nat6KYFWxRCVoqPGB7jsd-4ES3_-ElFARLLYJHvkOpwsax8kQ4_wrg) Ninghui Li et al.; [RT: a Role-based Trust-management framework](https://ieeexplore.ieee.org/abstract/document/1194885?casa_token=Hur5B31um3YAAAAA:P4LyjDr2SuqbOw7wXlnnHWpU8dyWeKr97PeV7OiQaHAxsGZP9Eelihh1h2AB65EGWziSValFhQ) Ninghui Li et al.

Chain discovery algorithms: [Distributed credential chain discovery in trust management](https://content.iospress.com/articles/journal-of-computer-security/jcs169) Ninghui Li et al.

Trans-organizational role-based access control: [RBAC-SC: Role-Based Access Control Using Smart Contract](https://ieeexplore.ieee.org/abstract/document/8307397) Cruz Li et al.

Off-chain computation: [On or Off the Blockchain? Insights on Off-Chaining Computation and Data](https://link.springer.com/chapter/10.1007/978-3-319-67262-5_1) Cruz Li et al.

