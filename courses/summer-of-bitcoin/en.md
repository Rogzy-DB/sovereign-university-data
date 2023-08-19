---
name: Building a Bitcoin Wallet
goal: Create your first bitcoin wallet on Android using BDK
objectives:
  - Undertsand and use BDK
  - Create your first bitcoin wallet
  - Undertsand all the programming component of a bitcoin transaction
---

# Create your first bitcoin wallet on Android using BDK

It is important to understand that simple and reused passwords can be easily hacked by hackers, who can exploit your personal information for malicious purposes.

To avoid this, we will show you how to use a secure password manager like Bitwarden and migrate your passwords from other storage services. We will address the importance of protecting your personal data, including using backups on external hard drives and pseudonyms to hide your online identity.

We will also discuss who is best positioned to protect the user: companies, regulation, or the user themselves.

Contributor team:

- Renaud Lifchitz; professor
- Thép Pantamis; professor
- Muriel; design
- Rogzy Noury & Fabian; production
- Théo; contribution

+++

# Chapter 1: All about BDK

![video](https://youtu.be/WoofLA70Edg)

# Chapter 2 - Setting up a basic skeleton app

![video](https://youtu.be/8T3Ge3ypPwE)

# Chapter 3 - Programming languages, bitcoin tools, BIP trivia

![video](https://youtu.be/pPrcWw0KZH4)

# Chapter 4 - Building Wallet and Repository objects

![video](https://youtu.be/Bf5bmAY5PG8)

This is where things get interesting on the bitcoin side of things. This task introduces 2 new objects: the Wallet object and the Repository object.

Both are initialized on startup by the SobiWalletApplication class, with some properties they need to function (wallet path and shared preferences respectively).

### Wallet object

The Wallet class is our window to the bitcoindevkit. It’s the only class that interacts with the bitcoindevkit direclty and you’ll find in there most of the API. Methods like createWallet(), loadExistingWallet(), and recoverWallet() allow you to generate/recover wallets on startup, and methods like sync(), getNewAddress(), and getBalance() provide the necessary interactions one would expect from a bitcoin library.

Note that because the bitcoindevkit is a native library (it is not written in Kotlin/Java and is provided as binaries to the OS), the library get “loaded” on initialization through the init block:

---

object Wallet {
private val lib: Lib

    init {
        // load bitcoindevkit native library
        Lib.load()
        lib = Lib()
    }
    // ...

## }

The library is then accessible throughout the class, and most methods use it like so:

---

fun getNewAddress(): String {
return lib.get_new_address(walletPtr)
}

fun getBalance(): Long {
return lib.get_balance(walletPtr)
}

---

The library comes with a few types (ExtendedKey, CreateTxResponse, SignResponse, etc.) which can be investigated by looking at the source code here.

### Repository object

The Repository design pattern is very common in Android applications. The idea is to create a layer of separation between the UI (activities, fragments) and the data they need to function. A Repository class is often used as the bridge between the two. For example, a fragment might need to query a list of friends the user has, and that list might be available from different locations (say a ping to a microservice, or a lookup in a local cache). It’s important to pull that sort of decision/code away from UI fragments. This is typically the sort of thing that the Repository will do; make decisions as to where and how to get data for the UI fragments that request it.

For us this shows up when the DispatchActivity tries to decide if the user already has a wallet initialized upon launch. In this case the activity simply asks the Repository the question

---

## Repository.doesWalletExist()

and doesn’t care how the Repository knows (in this example the repository uses a boolean value stored in shared preferences). Shared preferences are a way to store small amounts of data quickly without requiring a database. Common use cases are small strings and booleans (like choice of color theme, whether something has been completed, etc.).

### Using the bitcoindevkit

We can see the library in action through the logs, for example when creating a new wallet, or when pressing the new generateNewAddressButton on the receive fragment:

---

binding.generateNewAddressButton.setOnClickListener {
Log.i("SobiWallet", "${Wallet.getNewAddress()}")
}

---

# Chapter 5 - Implementing receive and sync

![video](https://youtu.be/kF6mkiYMSTg)

# Chapter 6 - Implementing send

![video](https://youtu.be/E9hOUm06ABM)

It's now time to connect the Wallet object to the user interface. Note how the "generate new address" button has an on onClick parameter that triggers the updateAddress() method on the viewmodel:

// ReceiveScreen.kt

Button(
onClick = { addressViewModel.updateAddress() },
colors = ButtonDefaults.buttonColors(DevkitWalletColors.auroraGreen),
shape = RoundedCornerShape(16.dp),
) {
Text(
text = "generate new address",
fontSize = 14.sp,
)
}

This viewmodel in turns calls the Wallet.getLastUnusedAddress(), which itself is a simple call to the bitcoin dev kit wallet object:

// Wallet.kt

object Wallet {
// ...

    fun getLastUnusedAddress(): String = wallet.getLastUnusedAddress()

}

QR codes

QR codes are generated using a library called zxing (you'll find the dependency in the /app/build.gradle.kts file).
Sync

The sync functionality in Devkit Wallet is very simple (Wallet.sync() will do). The sync is a call to the blockstream testnet public Electrum server. But note that we also wish to update the UI to reflect the current balance upon sync, and this is done using something called the viewmodel, a very common pattern in Android applications. ViewModels are a way to implement the observer pattern.

Take a look at the WalletViewModel class:

class WalletViewModel() : ViewModel() {

    private var _balance: MutableLiveData<ULong> = MutableLiveData(0u)
    val balance: LiveData<ULong>
        get() = _balance

    fun updateBalance() {
        Wallet.sync()
        _balance.value = Wallet.getBalance()
    }

}

Fragment and activities can simply "observe" (subscribe to) particular variables in our ViewModel, and the ViewModel will update them as this value changes. This ensures that the balance displayed in the composable is always up to date with the balance in the WalletViewModel. Easy peasy bitcoineesy.

# Chapter 7 - Adding transaction history

![video](https://youtu.be/37L82vt66YI)

# Chapter 8 - Displaying recovery phrase

![video](https://youtu.be/jqTtWPh573E)

# Chapter 9 - Recovering a wallet

![video](https://youtu.be/CNJrzZPQHpg)

# Chapter 10 - QnA

![video](https://youtu.be/FkSpTlFjbQ4)
