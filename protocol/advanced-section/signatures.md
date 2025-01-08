# Signatures

Papaya stands out for its advanced capabilities in electronic signatures and multi-operability, leveraging technologies such as bySig, permitAndCall from [1inch](https://github.com/1inch/solidity-utils), and multicall from [OpenZeppelin](https://github.com/OpenZeppelin/openzeppelin-contracts) libraries.

The 1inch libraries facilitate the creation of signatures capable of invoking any public Papaya method. Executors of these signatures can also earn rewards via the `sponsoredCall` method.

For examples of signature creation, please refer to our repository or [SDK](broken-reference).

{% hint style="info" %}
The main advantage of these technologies is that it is possible to invoke any available method (i.e: every getter/setter or both at once) using an electronic signature
{% endhint %}
