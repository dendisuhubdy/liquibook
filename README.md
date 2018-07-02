# Liquibook Implementation with CMake

Liquibook is an open source order matching engine from Object Computing (OCI).
The original repository is here https://github.com/objectcomputing/liquibook/.
The whole liquibook repository is a header-only library, but it seems that without
knowledge about build systems and computer science people could not easily plug-and
play liquibook. Bitwyre Technologies LLC decided to change that by moving to the 
CMake build system rather than the mwc build system (who uses that anyway). 

Liquibook provides the low-level components that make up an order matching engine.
Order matching is the process of accepting buy and sell orders for a security (or 
other fungible asset) and matching them to allow trading between parties who are 
otherwise unknown to each other.

An order matching engine is the heart of every financial exchange, and may be used
in many other circumstances including trading non-financial assets, serving as a 
test-bed for trading algorithms, etc.

The liquibook engine fits in the matching engine framework like this 

## Design
![alt text](https://github.com/objectcomputing/liquibook/raw/master/doc/Images/MarketApplication.png "Matching Engine")

In addition to the order matching process itself, Liquibook can be configured
to maintain an "depth book" that records the number of open orders and total quantity
represented by those orders at individual price levels.  

#### Example of an depth book
* Symbol XYZ: 
  * Buy Side: 
    * $53.20 per share: 1203 orders; 150,398 shares.
    * $53.19 per share: 87 orders; 63,28 shares
    * $52.00 per share 3 orders; 2,150 shares
  * Sell Side
    * $54.00 per share 507 orders; 120,700 shares
    * etc...            

## Order properties supported by Liquibook.

Liquibook is aware of the following order properties.

* Side: Buy or Sell
* Quantity
* Symbol to represent the asset to be traded
  * Liquibook imposes no restrictions on the symbol.  It is treated as a simple character string.
* Desired price or "Market" to accept the current price defined by the market.
  * Trades will be generated at the specified price or any better price (higher price for sell orders, lower price for buy orders)
* Stop loss price to hold the order until the market price reaches the specified value.
  * This is often referred to as simply a stop price.
* All or None flag to specify that the entire order should be filled or no trades should happen.
* Immediate or Cancel flag to specify that after all trades that can be made against existing orders on the market have been made, the remainder of the order should be canceled.
  * Note combining All or None and Immediate or Cancel produces an order commonly described as Fill or Kill.

The only required propoerties are side, quantity and price.  Default values are available for the other properties.

The application can define addtional properties on the order object as necessary.  These properties will have no impact on the behavior of Liquibook.
 
## Operations on Orders

In addition to submitting orders, traders may also submit requests to cancel or modify existing orders.  (Modify is also know as cancel/replace)
The requests may succeed or fail depending on previous trades executed against the order.
  
## Feedback Notifications

Liquibook will notify the application when significant events occur to allow the application to actually execute the trades identified by Liquibook, and to allow the application to publish market data for use by traders.

The notifications generated include:

* Notifications intended for trader submitting an order:
  * Order accepted 
  * Order rejected
  * Order filled (full or partial)
  * Order replaced
  * Replace request rejected
  * Order canceled
  * Cancel request rejected.
* Notifications intended to be published as Market Data
  * Trade
    * Note this should also trigger the application to do what it needs to do to make the trade happen.
  * Security changed
    * Triggered by any event that effects a security
      * Does not include rejected requests.
  * Notification of changes in the depth book (if enabled)
    * Depth book changed
    * Best Bid or Best Offer (BBO) changed.

## Performance
* Liquibook is written in C++ using modern, high-performance techniques. This repository includes
the source of a test program that can be used to measure Liquibook performance.
  * Benchmark testing with this program shows sustained rates of  
__2.0 million__ to __2.5 million__ inserts per second. 

As always, the results of this type of performance test can vary depending on the hardware and operating system on which you run the test, so use these numbers as a rough order-of-magnitude estimate of the type of performance your application can expect from Liquibook. 

## Design Adjustments
* Allows an application to use smart or regular pointers to orders.
* Compatible with existing order model, 
  * Requires a trivial interface which can be added to or wrapped around an existing Order object.
* Compatible with existing identifiers for securities, accounts, exchanges, orders, fills

## Example
This repository contains two complete example programs.  These programs can be used to evaluate Liquibook to see if it meets your needs. They can also be used as models for your application or even incorporated directly into your application thanks to the liberal license under which Liquibook is distributed.
