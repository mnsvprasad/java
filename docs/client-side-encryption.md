# Client-side encryption

The JSON representation of your workspace is stored on the Structurizr servers using AES encryption with a 128-bit key, a random salt and a server-side passphrase. For additional peace of mind, if you're a [paid plan](https://structurizr.com/pricing) customer, you can choose to encrypt your workspace with your own passphrase on the client before uploading it to Structurizr. In order to view a client-side encrypted workspace, you will be asked to enter your passphrase when you open the workspace in your web browser. The passphrase is then used to decrypt the workspace in your web browser - at no point does the passphrase leave your computer.

To use client-side encryption, simply create an instance of ```AesEncryptionStrategy``` and associate it with your ```StructurizrClient``` instance. For example:

```java
StructurizrClient structurizrClient = new StructurizrClient("key", "secret");
EncryptionStrategy encryptionStrategy = new AesEncryptionStrategy("password");
structurizrClient.setEncryptionStrategy(encryptionStrategy);

// upload your workspace as usual
structurizrClient.putWorkspace(1234, workspace);
```

The default key size is 128 bits and the default iteration count is 1000. An alternative constructor for <code>AesEncryptionStrategy</code> takes the following parameters:

- The key size (number of bits; e.g. 128, 192 or 256).
- The iteration count (used when generating keys).
- The passphrase.

In addition, a random salt and initialization vector are generated automatically for you, using Java's ```SecureRandom``` class.