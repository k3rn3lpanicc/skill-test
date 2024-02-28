# Skill Test project

Issues Fixed so far:

- Syntax errors:
    - Sql error in `new_mgldefi.sql`: fixed in [this commit](https://github.com/k3rn3lpanicc/skill-test/commit/c89f4bf908e9d0994e2f78a7063cf58e8a2c744b)

    - columnSet was not defined in `common.utils.js`: fixed in [this commit](https://github.com/k3rn3lpanicc/skill-test/commit/246f0171228f6525e9babd5e3d17fd3f0b69f9ff)

- Forget password validation issue: The `/user/forgotpassword` route did not have a validation functionality, this lead to a situation where the given email address was not normalized and _victor.hugo@peiko.com_ would be different from _victorhugo@peiko.com_ despite them be equal and this lead to inconsistency (since the registered email would be saved as normalized email - with no dots - but the email that forget password deals with searchs for a email - with a dot - ): fixed in [this commit](https://github.com/k3rn3lpanicc/skill-test/commit/9a9f04ee4d382bcace7452239ea676d10a1ebedb)
- Gas price estimation in `Wallet - Send Tokens`: The project did a good job on finding the estimated gas used in a transaction, not so good on the `gas price` part, the `gas price` was set to 30 by default which lead to pending and never accepting transactions on Polygon, I've wrote a helper utility and modified the front-end project to put the current gas price of the network in the SendModal so the user won't have to worry about pending transactions: fixed in [this commit](https://github.com/k3rn3lpanicc/skill-test/commit/701a20512a3f246dfd0e8e39b090470493dda61c)

Issues that I've encountered with (and probably will be fixed soon):

- The Token type in the `Wallet - Send Tokens` sections is not correct, it has only these states: `ERC20`, `BEP20`, `UNKNOWN`. But the MATIC and BNB tokens are neither `ERC20` like nor unknown, they are `Native` tokens which is not included.
- The private key of the wallet is stored in DB without encryption, this is not a good practice since if the backend has any vulnerability, that could led to lots of financial loss if hacked, the better practice is to encrypt the private key of the user with the password they choose, save the Hash(password) in user table, and ask the user his/her password when we want to do something with their wallet and decrypt the encrypted private key using the user's password and go on.
- Memo is not included: In the Send section of the wallet, despite the transaction works and sends tokens as intended, the Memo part is not neither in the call to back-end nor in the transaction itself.
- The network would change from Polygon to Binance when we refresh the page, its not a big deal but of course it would be annoying for the end user.


# How to run the project

Run `yarn install` in the root folder, also in the `/backend` folder to get all the packages you need.

Then you can either run the back-end and front-end seprately (by running `yarn run client` on the front-end side and `yarn run dev` on the back-end side), or you can run them both by running `yarn run dev` in the root folder.
