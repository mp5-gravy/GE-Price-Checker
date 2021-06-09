# GE Price Checker

This is a util class that I wrote/refactored based on a couple snippets I found searching through the dreambot forum


Uses the endpoint ```https://services.runescape.com/m=itemdb_oldschool/api/catalogue/detail.json?item=``` to retrieve and parse the item info.

It will cache the result for set amount of time to reduce http requests.


The item name -> id hash map is hard coded and taken from one of the random snippets I found on the forums so it may be outdated. If someone opens an issue/ makes a pr/ or contacts me with something missing/broken I will fix it.


## Usage

### Object instantiation
```java
// default cache is 10 minutes, or you can construct it with your own timeout long. 
// ie: new PriceChecker(300000) would store cache for 5 minutes.
PriceChecker pc = new PriceChecker(); 
```

## Object usage

### price lookup
```java 
PriceChecker pc = new PriceChecker(); 
int runeScimmyPrice = pc.lookupPrice("Rune scimitar");
```

### ge info lookup

```java 
PriceChecker pc = new PriceChecker(); 
GELookupResult runeScimmyResult = pc.lookup("Rune scimitar");
```
This is the GELookupResult object shape -
```java 
public static final class GELookupResult {
    public final String smallIconUrl, largeIconUrl, type, typeIcon, name, itemDescription;
    public final boolean isMembers;
    public final int id, price;
}
```

### networth lookup
#### can lookup either in player inventory, in player bank, or on player equipment

```java
PriceChecker pc = new PriceChecker(); 
int bankWorthOfRuneScimitars = pc.getOurItemsWorthFromBank("Rune scimitar");
int inventoryWorthOfRuneScimitars = pc.getOurItemsWorthFromInventory("Rune scimitar");
int equipmentWorthOfRuneScimitars = pc.getOurItemsWorthFromEquipment("Rune scimitar"); 
```
or if you just want the total
```java
PriceChecker pc = new PriceChecker(); 
int totalWorthOfRuneScimitars = pc.getOurItemsWorthTotal("Rune scimitar");
```