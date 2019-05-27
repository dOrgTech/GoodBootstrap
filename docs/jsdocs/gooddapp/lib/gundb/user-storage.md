<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### Table of Contents

-   [GunDBUser][1]
    -   [Properties][2]
-   [FieldPrivacy][3]
-   [ProfileField][4]
    -   [Properties][5]
-   [FeedEvent][6]
    -   [Properties][7]
-   [TransactionEvent][8]
-   [getReceiveDataFromReceipt][9]
    -   [Parameters][10]
-   [UserStorage][11]
    -   [Parameters][12]
    -   [wallet][13]
    -   [gunuser][14]
    -   [profile][15]
    -   [feed][16]
    -   [feedIndex][17]
    -   [user][18]
    -   [ready][19]
    -   [init][20]
    -   [getFeedItemByTransactionHash][21]
        -   [Parameters][22]
    -   [getAllFeed][23]
    -   [getProfileFieldValue][24]
        -   [Parameters][25]
    -   [getProfileField][26]
        -   [Parameters][27]
    -   [getDisplayProfile][28]
        -   [Parameters][29]
    -   [getPrivateProfile][30]
        -   [Parameters][31]
    -   [setProfile][32]
        -   [Parameters][33]
    -   [setProfileField][34]
        -   [Parameters][35]
    -   [indexProfileField][36]
        -   [Parameters][37]
    -   [setProfileFieldPrivacy][38]
        -   [Parameters][39]
    -   [getFeedPage][40]
        -   [Parameters][41]
    -   [getFormattedEvents][42]
        -   [Parameters][43]
    -   [getUserAddress][44]
        -   [Parameters][45]
    -   [getUserProfile][46]
        -   [Parameters][47]
    -   [formatEvent][48]
        -   [Parameters][49]
    -   [enqueueTX][50]
        -   [Parameters][51]
    -   [dequeueTX][52]
        -   [Parameters][53]
    -   [peekTX][54]
        -   [Parameters][55]
    -   [updateFeedEvent][56]
        -   [Parameters][57]
    -   [getLastBlockNode][58]
    -   [saveLastBlockNumber][59]
        -   [Parameters][60]
    -   [deleteAccount][61]
    -   [maskField][62]
        -   [Parameters][63]
    -   [Parameters][64]

## GunDBUser

User details returned from Gun SEA

Type: {alias: [string][65], epub: [string][65], pub: [string][65], sea: any}

### Properties

-   `alias` **[string][65]** 
-   `epub` **[string][65]** 
-   `pub` **[string][65]** 
-   `sea` **any** 

## FieldPrivacy

possible privacy level for profile fields

Type: (`"private"` \| `"public"` \| `"masked"`)

## ProfileField

User's profile field data

Type: {value: EncryptedField, display: [string][65], privacy: [FieldPrivacy][66]}

### Properties

-   `value` **EncryptedField** 
-   `display` **[string][65]** 
-   `privacy` **[FieldPrivacy][66]** 

## FeedEvent

User's feed event data

Type: {id: [string][65], type: [string][65], date: [string][65], data: any}

### Properties

-   `id` **[string][65]** 
-   `type` **[string][65]** 
-   `date` **[string][65]** 
-   `data` **any** 

## TransactionEvent

Blockchain transaction event data

Type: any

## getReceiveDataFromReceipt

Extracts transfer events sent to the current account

### Parameters

-   `receipt` **[object][67]** Receipt event

Returns **[object][67]** {transferLog: event: [{evtName: evtValue}]}

## UserStorage

Users gundb to handle user storage.
User storage is used to keep the user Self Soverign Profile and his blockchain transcation history

### Parameters

-   `wallet` **GoodWallet** 

### wallet

wallet an instance of GoodWallet

Type: GoodWallet

### gunuser

a gun node refering to gun.user()

Type: Gun

### profile

a gun node refering to gun.user().get('profile')

Type: Gun

### feed

a gun node refering to gun.user().get('feed')

Type: Gun

### feedIndex

In memory array. keep number of events per day

Type: [Array][68]&lt;\[[Date][69], [number][70]]>

### user

object with Gun SEA user details

Type: [GunDBUser][71]

### ready

A promise which is resolved once init() is done

Type: [Promise][72]&lt;[boolean][73]>

### init

Initialize wallet, gundb user, feed and subscribe to events

### getFeedItemByTransactionHash

Find feed by transaction hash in array, and returns feed object

#### Parameters

-   `transactionHash` **[string][65]** transaction identifier

Returns **[object][67]** feed item or null if it doesn't exist

### getAllFeed

Returns a Promise that, when resolved, will have all the feeds available for the current user

Returns **[Promise][72]&lt;[Array][68]&lt;[FeedEvent][74]>>** 

### getProfileFieldValue

Returns profile attribute

#### Parameters

-   `field` **[string][65]** Profile attribute

Returns **[string][65]** Decrypted profile value

### getProfileField

Returns progfile attribute value

#### Parameters

-   `field` **[string][65]** Profile attribute

Returns **[Promise][72]** Gun profile attribute object

### getDisplayProfile

Return display attribute of each profile property

#### Parameters

-   `profile` **[object][67]** User profile

Returns **[object][67]** User model with display values

### getPrivateProfile

Returns user model with attribute values

#### Parameters

-   `profile` **[object][67]** user profile

Returns **[object][67]** UserModel with some inherit functions

### setProfile

Save profile with all validations and indexes
It saves only known profile fields

#### Parameters

-   `profile` **UserModel** User profile


-   Throws **any** Error if profile is invalid

Returns **[Promise][72]** Promise with profile settings updates and privacy validations

### setProfileField

Set profile field with privacy settings

#### Parameters

-   `field` **[string][65]** Profile attribute
-   `value` **[string][65]** Profile attribute value
-   `privacy` **[string][65]** (private | public | masked) (optional, default `'public'`)

Returns **[Promise][72]** Promise with updated field value, secret, display and privacy.

### indexProfileField

Generates index by field if privacy is public, or empty index if it's not public

#### Parameters

-   `field` **[string][65]** Profile attribute
-   `value` **[string][65]** Profile attribute value
-   `privacy` **[string][65]** (private | public | masked)

Returns **[Promise][72]&lt;ACK>** Gun result promise after index is generated

### setProfileFieldPrivacy

Set profile field privacy.

#### Parameters

-   `field` **[string][65]** Profile attribute
-   `privacy` **[string][65]** (private | public | masked)

Returns **[Promise][72]** Promise with updated field value, secret, display and privacy.

### getFeedPage

Returns the next page in feed. could contain more than numResults. each page will contain all of the transactions
of the last day fetched even if > numResults

#### Parameters

-   `numResults` **[number][70]** return at least this number of results if available
-   `reset` **[boolean][73]** should restart cursor (optional, default `false`)

Returns **[Promise][72]** Promise with an array of feed events

### getFormattedEvents

Return all feed events

#### Parameters

-   `numResults` **[number][70]** 
-   `reset` **[boolean][73]** 

Returns **[Promise][72]** Promise with array of standarised feed events

### getUserAddress

#### Parameters

-   `field` **[string][65]** Profile field value (email, mobile or wallet address value)

Returns **[string][65]** address

### getUserProfile

Returns name and avatar from profile based filtered by received value

#### Parameters

-   `field` **[string][65]** Profile field value (email, mobile or wallet address value)

Returns **[object][67]** profile - { name, avatar }

### formatEvent

Returns the feed in a standard format to be loaded in feed list and modal

#### Parameters

-   `param` **[FeedEvent][74]** Feed event with data, type, date and id props
    -   `param.data`  
    -   `param.type`  
    -   `param.date`  
    -   `param.id`  

Returns **[Promise][72]** Promise with StandardFeed object,
 with props { id, date, type, data: { amount, message, endpoint: { address, fullName, avatar, withdrawStatus }}}

### enqueueTX

enqueue a new pending TX done on DAPP, to be later merged with the blockchain tx
the DAPP event can contain more details than the blockchain tx event

#### Parameters

-   `event` **[FeedEvent][74]** 

Returns **[Promise][72]&lt;>** 

### dequeueTX

remove and return pending TX

#### Parameters

-   `eventId` **[string][65]** 
-   `event` **any** 

Returns **[Promise][72]&lt;[FeedEvent][74]>** 

### peekTX

lookup a pending tx

#### Parameters

-   `eventId` **[string][65]** 

Returns **[Promise][72]&lt;[FeedEvent][74]>** 

### updateFeedEvent

Update feed event

#### Parameters

-   `event` **[FeedEvent][74]** Event to be updated

Returns **[Promise][72]** Promise with updated feed

### getLastBlockNode

Returns the 'lastBlock' gun's node

Returns **any** 

### saveLastBlockNumber

Saves block number in the 'lastBlock' node

#### Parameters

-   `blockNumber` **([number][70] \| [string][65])** 

Returns **[Promise][72]&lt;([Promise][72]&lt;any> | [Promise][72]&lt;(R | any)>)>** 

### deleteAccount

Delete the user account.
Deleting gundb profile and clearing local storage
Calling the server to delete their data

Returns **[Promise][72]&lt;[boolean][73]>** 

### maskField

Returns phone with last 4 numbers, and before that \*\*\*,
and hide email user characters leaving visible only first and last character

#### Parameters

-   `fieldType` **[string][65]** (Email, mobile or phone) Field name
-   `value` **[string][65]** Field value

Returns **[string][65]** Returns masked value with \*\*\* to hide characters

## 

Clean string removing blank spaces and special characters, and converts to lower case

### Parameters

-   `field` **[string][65]** Field name
-   `value` **[string][65]** Field value

Returns **[string][65]** Value without '+' (plus), '-' (minus), '\_' (underscore), ' ' (space), in lower case

[1]: #gundbuser

[2]: #properties

[3]: #fieldprivacy

[4]: #profilefield

[5]: #properties-1

[6]: #feedevent

[7]: #properties-2

[8]: #transactionevent

[9]: #getreceivedatafromreceipt

[10]: #parameters

[11]: #userstorage

[12]: #parameters-1

[13]: #wallet

[14]: #gunuser

[15]: #profile

[16]: #feed

[17]: #feedindex

[18]: #user

[19]: #ready

[20]: #init

[21]: #getfeeditembytransactionhash

[22]: #parameters-2

[23]: #getallfeed

[24]: #getprofilefieldvalue

[25]: #parameters-3

[26]: #getprofilefield

[27]: #parameters-4

[28]: #getdisplayprofile

[29]: #parameters-5

[30]: #getprivateprofile

[31]: #parameters-6

[32]: #setprofile

[33]: #parameters-7

[34]: #setprofilefield

[35]: #parameters-8

[36]: #indexprofilefield

[37]: #parameters-9

[38]: #setprofilefieldprivacy

[39]: #parameters-10

[40]: #getfeedpage

[41]: #parameters-11

[42]: #getformattedevents

[43]: #parameters-12

[44]: #getuseraddress

[45]: #parameters-13

[46]: #getuserprofile

[47]: #parameters-14

[48]: #formatevent

[49]: #parameters-15

[50]: #enqueuetx

[51]: #parameters-16

[52]: #dequeuetx

[53]: #parameters-17

[54]: #peektx

[55]: #parameters-18

[56]: #updatefeedevent

[57]: #parameters-19

[58]: #getlastblocknode

[59]: #savelastblocknumber

[60]: #parameters-20

[61]: #deleteaccount

[62]: #maskfield

[63]: #parameters-21

[64]: #parameters-22

[65]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String

[66]: #fieldprivacy

[67]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object

[68]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array

[69]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Date

[70]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number

[71]: #gundbuser

[72]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise

[73]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean

[74]: #feedevent
## Source
[https://github.com/GoodDollar/GoodDAPP/src/lib/gundb/UserStorage.js](https://github.com/GoodDollar/GoodDAPP/src/lib/gundb/UserStorage.js)
