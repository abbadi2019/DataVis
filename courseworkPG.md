---
id: litvis

narrative-schemas:
  - ../narrative-schemas/courseworkPG.yml

elm:
  dependencies:
    gicentre/elm-vegalite: latest
    gicentre/tidy: latest
---

@import "../css/datavis.less"

```elm {l=hidden}
import Tidy exposing (..)
import VegaLite exposing (..)
```

# Postgraduate Coursework

## Introduction

With the growth of usage for Internet of Things (IoT) devices in the world, the lack of security for them is the main issue. The vulnerability of IoT devices is major, and the purpose of this research is set to narrow/reduce them. In 2015 it was estimated that 5 to 9 billion connected IoT devices are available with a growth of 17% yearly [1]

{(questions|}

- How many IoT devices are infected worldwide.
- What are the weakest protocols to infect IoT devices.
- What type of attacks are carried on IoT devices.

{|questions)}

The above research questions have helped me shape the upcoming visualisations as to assist me answer them.

{(visualization|}

In this section, I will insert my visualisation types I used to answer my research question.

### Pie Chart represents type of Protocols are most vulnerable

```elm {l=hidden}
birdData =
    toPolar
        [ ( "Telnet", 75.4 )
        , ( "SSH", 11.59 )
        , ( "HTTP", 5.53 )
        , ( "8291", 3.41 )
        , ( "8080", 2.57 )
        , ( "7547", 1.51 )
        , ( "Others", 1.5 )
        ]
```

```elm {v}
pieExample : Spec
pieExample =
    let
        cfg =
            configure
                << configuration (coView [ vicoStroke Nothing ])
    in
    toVegaLite [ cfg [], layer [ pie birdData ] ]
```

### GeoMap of IoT Devices infected via Telnet

<a href="https://ibb.co/n6fGjdt"><img src="https://i.ibb.co/34W3c6Q/Map-Via-Telnetv1.jpg" alt="Map-Via-Telnetv1" border="0"></a>

### GeoMap of IoT Devices infected via SSH

<a href="https://ibb.co/zhFPRQg"><img src="https://i.ibb.co/VWxMSJG/Map-Via-SSHv1.jpg" alt="Map-Via-SSHv1" border="0"></a>

{|visualization)}

{(insights|}

In this section, will illustrate how the above visualisation have allowed me to discover about the datasets and answer the research questions. Many of these attacks on IoT devices are used by Brute-force, which attempting to attack devices by trying millions of passwords which manufactures are working towards tackling.

#### Pie Chart

Based on the [data table](https://raw.githubusercontent.com/abbadi2019/DataVis/master/Pie_IoT.csv) shown below, the pie chart indicates that the most vulnerable protocol is Telnet that can allow IoT devices to be infected with huge percentage and difference to the second most protocol that is used to infect the IoT devices which is SSH. Both of these protocol are usually used to remote into devices from distance, hence the high vulnerablitities and easy for attackers to expolit.

```elm {l=hidden}
attacksOnIoTTable : Table
attacksOnIoTTable =
    """Protocol,Percentage
      Telnet,75.4
      SSH,11.59
      HTTP,5.53
      8291,3.41
      8080,2.57
      7547,1.51
      Others,1.5"""
        |> fromCSV
```

^^^elm{m=(tableSummary 7 attacksOnIoTTable)}^^^

#### GeoMap for Telnet

Here, the [data table](https://raw.githubusercontent.com/abbadi2019/DataVis/master/Telnet_IoT.csv) shows the most infected countries and here we have chosen the top 10. This illustrates that Brazil is the lead country to have infected IoT devices using Telnet protocol, even though someone would think there should not be much IoT devcies in those regions. Not far off, China comes second which I expected to be higher than Brazil comparing its population numbers, and third and fourth (Japan & Russia) are not far of from each other that I also to have more infected IoT devices specially in Russia due to its high population.

```elm {l=hidden}
ioTviaTelnetTable : Table
ioTviaTelnetTable =
    """Country,Percentage
      Brazil,23.38
      China,17.22
      Japan,8.64
      Russia,7.22
      USA,4.55
      Mexico,3.78
      Greece,3.51
      South Korea,3.32
      Turkey,2.61
      India,1.71"""
        |> fromCSV
```

^^^elm{m=(tableSummary 10 ioTviaTelnetTable)}^^^

#### GeoMap for SSH

Here, the [data table](https://raw.githubusercontent.com/abbadi2019/DataVis/master/SSH_IoT.csv) illustrates a different dataset which shows that SSH is totally different than Telnet. Some countries had highly infected IoT devices through Telnet and are less in SSH. As it can be seen that Brazil has dropped to sixth place and China takes the lead as the most infected IoT devices via this protocol. And suprisingly, Vietnam has come second and not far of USA is in third place as the top three contries that show vulnerabilities in IoT devices.

```elm {l=hidden}
ioTviaSSHTable : Table
ioTviaSSHTable =
    """Country,Percentage
      China,15.77
      Vietnam,11.38
      USA,9.78
      France,5.54
      Russia,4.53
      Brazil,4.22
      Germany,4.01
      South Korea,3.39
      India,2.86
      Romania,2.231"""
        |> fromCSV
```

^^^elm{m=(tableSummary 10 ioTviaSSHTable)}^^^

{|insights)}

{(designJustification|}

In this section, I will discuss how careful my designs were considered to have major imapct to readers. Will start by justfying the the chosen colours, layout and how they can interact with each other.

### Colour

Here, I will demonstrate how the colour coding are chosing. For the pie chart, used darker colour for the most perecentage of vulnerable protocols then the colours become lighter as the percentage is decreased. For the GeoMap visuals, I have used darker colours for the countries are most infected and the colour thickness started to reduce as the perecentage number of infected contries are recorded.

### Layout

The layout chosen is best visual to demonstrate the given datasets. Along with the types used suchg as Pie Chart where it will be less visual if used as bar chart, specially for this specific datasets. Whereas, for GeoMaps there is not an alternative way to demonstrate them as these answer my research questions.

### Interactions

For this part, is to identify how the chosen visualisations interact for others to maniuplate and/or amend the datasets. In this coursework, the only interactive visual is the Pie Chart as the data can be amended and it will be previewed once saved. Whereas for the GeoMaps, unforunatley I have tried to make them as interacted as possible but instead I have used Geojson.io to produce my viuslisations map along with the colour codes as I have uploaded those to github. Therefore, I have used the produced map, and added the link here to view as normal for the purpose of this coursework.

{|designJustification)}

{(validation|}

Further work I can introduce if this exercise was asked to be carried out again, is to identify how long it can take to detect attack on IoT devices using intrusion detection systems. Will produce the following Barchart:
<a href="https://ibb.co/rx5KtBw"><img src="https://i.ibb.co/T4PDTQg/Validation-Bar-Chart.jpg" alt="Validation-Bar-Chart" border="0"></a>
The bar chart illustratestates the number of minutes before each of the five attackers that were detected actually were detected. The average number of minutes before the attacks were detected was six hours and 41 minutes. The first attack that was detected was detected 5 hours and 36 minutes after the attack was introduced. The last attack that was detected was 7 hours and 41 minutes after the attack was introduced.

Many takeways from the visualisations introduced in this coursework, as I identified the countries that are mostly infected using certain protocols by using Brut-force passwords approaches. The colour codes, layout and interaction are my main strengths but I have had few obstacles in creating the GeoMaps to code within Litviz.

{|validation)}

{(references|}

**Haroz, S., and Whitney, D.** (2012) How capacity limits of attention influence information visualization effectiveness. _IEEE Transactions on Visualization and Computer Graphics_, 18(12) pp.2402-2410.

[1] **Sheth, A.** (2016). Internet of Things to Smart IoT Through Semantic, Cognitive, and Perceptual Computing. _IEEE Intelligent Systems_, 31(2), pp.108-112.

**Borkin, M., Vo, A., Bylinskii, Z., Isola, P., Sunkavalli, S., Oliva, A. and Pfister, H.** (2013) [What makes a visualization memorable?](https://vcg.seas.harvard.edu/publications/what-makes-a-visualization-memorable/paper) _IEEE Transactions on Visualization and Computer Graphics_, 19(12), pp.2306-2315.

{|references)}

---

<!-- Appendix: Code for producing radial (pie) charts using an azimuthal map projection -->

```elm{l=hidden}
radialAxes : Spec
radialAxes =
    asSpec
        [ dataFromJson (geometry (graticule 30) []) []
        , projection [ prType azimuthalEquidistant, prRotate 0 90 0 ]
        , geoshape [ maStrokeWidth 0.2, maFilled False ]
        ]


pie : Spec -> Spec
pie =
    stack [ prType azimuthalEquidistant, prRotate 0 90 0 ]


donut : Spec -> Spec
donut geoData =
    let
        circleCoords lat =
            List.map (\x -> ( toFloat (x * 10), toFloat lat )) (List.range 0 36)

        pieSpec =
            asSpec
                [ dataFromJson geoData [ jsonProperty "features" ]
                , geoshape [ maStroke "white", maStrokeWidth 3 ]
                , encoding
                    (color
                        [ mName "properties.cat"
                        , mMType Nominal
                        , mLegend [ leTitle "" ]
                        ]
                        []
                    )
                ]

        blankSpec =
            asSpec
                [ dataFromJson (geometry (geoPolygon [ circleCoords 30 ]) []) []
                , geoshape [ maFill "#fff" ]
                ]
    in
    asSpec
        [ projection [ prType azimuthalEquidistant, prRotate 0 90 0 ]
        , layer [ pieSpec, blankSpec ]
        ]


rose : Spec -> Spec
rose geoData =
    let
        gratSpec =
            asSpec
                [ dataFromJson (geometry (graticule 22.5) []) []
                , geoshape [ maStrokeWidth 0.2, maFilled False ]
                ]

        roseSpec =
            asSpec
                [ dataFromJson geoData [ jsonProperty "features" ]
                , geoshape [ maFillOpacity 0.7, maStroke "#fff", maStrokeWidth 4 ]
                , encoding (color [ mStr "#ccc" ] [])
                ]
    in
    asSpec
        [ projection [ prType azimuthalEquidistant, prRotate 202 -90 0 ]
        , layer [ roseSpec, gratSpec ]
        ]


range : Float -> Float -> Float -> List Float
range mn mx step =
    List.range 0 ((mx - mn) / step |> round)
        |> List.map (\x -> mn + (toFloat x * step))


scanl : (a -> b -> b) -> b -> List a -> List b
scanl fn b =
    let
        scan a bs =
            case bs of
                hd :: tl ->
                    fn a hd :: bs

                _ ->
                    []
    in
    List.foldl scan [ b ] >> List.reverse


graticule : Float -> Geometry
graticule gStep =
    let
        meridian lng =
            List.map (\lat -> ( lng, lat )) (range (gStep - 90) (90 - gStep) (min 5 gStep))

        parallel lat =
            List.map (\lng -> ( lng, lat )) (range -180 180 (min 10 gStep))
    in
    geoLines
        (List.map parallel (range (gStep - 90) (90 - gStep) gStep)
            ++ List.map meridian (range -180 180 gStep)
        )


toPolar : List ( String, Float ) -> Spec
toPolar pairs =
    case pairs of
        [] ->
            -- Invisible polygon if no data provided.
            geoFeatureCollection [ geometry (geoPolygon [ [ ( 0, 90 ), ( 1, 90 ), ( 0, 90 ) ] ]) [ ( "cat", str "" ) ] ]

        [ ( label, _ ) ] ->
            -- Full circle if singleton provided.
            geoFeatureCollection
                [ geometry (geoPolygon [ [ ( 0, 90 ), ( 359.9, -89 ), ( 0, -89 ), ( 0, 90 ) ] ])
                    [ ( "cat", str label ) ]
                ]

        _ ->
            -- Segments if two or more data items provided.
            let
                geom ( a, b, label ) =
                    geometry (geoPolygon [ [ ( 0, 90 ), ( b, -89 ), ( a, -89 ), ( 0, 90 ) ] ])
                        [ ( "cat", str label ) ]

                adjacent xs =
                    List.map2 Tuple.pair xs (List.drop 1 xs ++ List.take 1 xs)

                triplet =
                    let
                        degs xs =
                            scanl (\a b -> 360 * a / List.sum xs + b) 0 xs
                    in
                    pairs
                        |> List.unzip
                        |> Tuple.second
                        |> degs
                        |> adjacent
                        |> List.map2 (\label ( a, b ) -> ( a, b, label )) (List.unzip pairs |> Tuple.first)
            in
            geoFeatureCollection (List.map geom triplet)


toRose : List ( String, Float ) -> Spec
toRose pairs =
    case pairs of
        [] ->
            -- Invisible polygon if no data provided.
            geoFeatureCollection [ geometry (geoPolygon [ [ ( 0, 90 ), ( 1, 90 ), ( 0, 90 ) ] ]) [ ( "cat", str "" ) ] ]

        [ ( label, _ ) ] ->
            -- Full circle if singleton provided.
            geoFeatureCollection
                [ geometry (geoPolygon [ [ ( 0, 90 ), ( 359.9, -89 ), ( 0, -89 ), ( 0, 90 ) ] ])
                    [ ( "cat", str label ) ]
                ]

        _ ->
            -- Segments if two or more data items provided.
            let
                geom ( ( a, b ), r, label ) =
                    geometry (geoPolygon [ [ ( 0, 90 ), ( b, r ), ( a, r ), ( 0, 90 ) ] ])
                        [ ( "cat", str label ) ]

                adjacent xs =
                    List.map2 Tuple.pair xs (List.drop 1 xs ++ List.take 1 xs)

                quad =
                    let
                        degs =
                            range 0 360 (360 / (List.length pairs |> toFloat))

                        maxR =
                            List.unzip pairs |> Tuple.second |> List.maximum |> Maybe.withDefault 1

                        rs =
                            List.unzip pairs |> Tuple.second |> List.reverse |> List.map (\r -> 80 - 169.9 * r / maxR)

                        labels =
                            List.unzip pairs |> Tuple.first |> List.reverse
                    in
                    degs |> adjacent |> List.map3 (\label r ab -> ( ab, r, label )) labels rs
            in
            geoFeatureCollection (List.map geom quad)


stack : List ProjectionProperty -> Spec -> Spec
stack proj geoData =
    asSpec
        [ configure (configuration (coView [ vicoStroke Nothing ]) [])
        , width 200
        , height 200
        , projection proj
        , dataFromJson geoData [ jsonProperty "features" ]
        , geoshape [ maStroke "#fff" ]
        , encoding (color [ mName "properties.cat", mMType Nominal, mLegend [ leTitle "" ] ] [])
        ]
```
