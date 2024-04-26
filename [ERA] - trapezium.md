## Micro-level description of an OP "trapezium"

This configuration is one of the most essential topologies in a double-track railway line as it allows all movements to be kept or shifted between Normal or Reversed operation. In essence the trapezium is a 4-points 4-signals V-configuration.

## Implementation and Topology

Assume the left signals to be `L1` and `L2`, and analogous for the right signals `R1` and `R2`. The trapezium allows routes from all left to all right signal's tracks. Four switches are part of the Trapezium, let us call them `PL1`, `PL2`, `PR1` and `PR2`, as they are all next to one signal.

The implementation layer describes WHAT constitutes the OP or SoL.

```
# Implementation of the trapezium

:Line1     a   era:NationalRailwayLine .

:OPT       a   era:OperationalPoint .   # era:AggregatedObject
:SOLLeft   a   era:SectionOfLine ;      # idem, but on the left side of the Trapezium
          era:nationalLine :Line1 .
:SOLRight  a   era:SectionOfLine ;      # for the right part
          era:nationalLine :Line1 .

:JT a era:Junction ;            # era:BasicObject
      era:isPartOf :OPT .

:Trapeze a era:SignalsGrid ;    # era:BasicObject
      era:isPartOf :OPT .

# TRACKS
:TL1 a era:Track ;              # era:BasicObject
      era:isPartOf :SOLLeft ;
      era:hasAbstraction :TL1t .

:TL2 a era:Track ;              # era:BasicObject
      era:isPartOf :SOLLeft ;
      era:hasAbstraction :TL2t .
# idem for the tracks on the right

# SIGNALS
:L1 a era:Signal ;
  era:belongsTo :Trapeze ;     # Signals form a SignalsGrid
  era:hasAbstraction :L1t .

:PL1 a era:Switch ;            # Switches form a Junction
  era:belongsTo :JT ;
  era:hasAbstraction :PL1t .

:L2 a era:Signal ...
:R1 a era:Signal ...
:R2 a era:Signal ...
```

In order to link the implementation to the topology, including their location in space and time, we use the classes from Topology. But we do not model the navigation on the level of the switches! We will model the Navigability of the Operational point *as a whole*.

```
# The Topology of the Trapezium: expressing how tracks connect to other tracks

:TL1t a era:LinearElement .
:TL2t a era:LinearElement .
:TR1t a era:LinearElement .
:TR2t a era:LinearElement .

:OPTt a era:NonlinearElement ; # the Trapezium as a whole
      era:navigate :OPT_routeL1R1 , :OPT_routeL1R2 , :OPT_routeL2R1 , :OPT_routeL2R2 .

:OPT_routeL1R1 a era:Navigability ;
    era:from :TL1t ;
    era:to :TR1t .

:OPT_routeL1R2 a era:Navigability ;
    era:from :TL1t ;
    era:to :TR2t .

:OPT_routeL2R1 a era:Navigability ;
    era:from :TL2t ;
    era:to :TR1t .

:OPT_routeL2R2 a era:Navigability ;
    era:from :TL2t ;
    era:to :TR2t ;
    era:validity :OPT_RouteL2R2_Outage .         # When a certain route is not available for a while

:OPT_RouteL2R2_Outage a era:TemporalFeature ;
... # limits in time on that route
```

For the exact positions of the switches and signals, we detail their topological abstractions.
```
:L1t a era:NonlinearElement ;
    era:hasImplementation :L1 ;
    era:hasPosition :Position_L1 .

:Position_L1 a era:SpotLocation ;
... # details of the location
```

For the TAFTAP aspects, we use the Implementation layer as started above, but grouped on the Operational Point itself:
```
:TrapezePrimaryLocation    a era:PrimaryLocation .
:OPT      era:primaryLocation :TrapezePrimaryLocation .
:SOLLeft  era:opStart  :OPT ;
          era:primaryLocation :OtherPL .
```




      

