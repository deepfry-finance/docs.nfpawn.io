Right now these documents are useful for developers.

But in the future they will be useful for developers AND brokers AND sellers



# NFPawn

People with NFTs ("**liquidators**") sell them for value tokens and have a limited-time offer to buyback (at a higher price).

These offers come from "**offerors**" that can take the NFT if the buyback offer expires.

And to keep things fun, if nobody acts then **anybody** can come in and buy NFTs that are sitting around.

Here is the main idea:

```
Offers are generated offline by Offeror. A Liquidator starts the process by
executing an offer. Here is what happens during that whole process, and during
this whole time an NFT is kept in custody by this contract. Time goes from left
to right.

           │              │              │
Offeror    │              │-Can take collateral-------------------------------->
           │              │              │
Liquidator │-Can buyback--+--------------+------------------------------------->
           │              │              │
Anybody    │              |              |-Can buyback------------------------->
           |              │              │
           ^ Offer        ^ Collateral    ^ Free
             execution      at risk         for all
             time           time            time!

             Liquidator
             loses NFT and
             gets value
             token
```

## More programmer details

[Cron Jobs.md](Cron Jobs.md)

[Database.md](Database.md)

