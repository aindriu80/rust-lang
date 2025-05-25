## Inbhréagnú: An bhféadfadh Patrún Teip a Mheaitseáil

Tagann patrúin i ndá fhoirm: inbhréagnaithe agus neamh-inbhréagnaithe. Is _neamh-inbhréagnaithe_ patrúin a mheaitseálfaidh
le haghaidh aon luach féideartha a rithtear. Sampla amháin is ea `x` sa
ráiteas `let x = 5;` mar go meaitseálann `x` aon rud agus dá bhrí sin ní féidir leis teip
a mheaitseáil. Is _neamh-inbhréagnaithe_ patrúin nach féidir leo meaitseáil le haghaidh luach féideartha éigin. Sampla amháin is ea `Some(x)` sa abairt `if let Some(x) =
a_value` mar mura bhfuil an luach san athróg `a_value` ach `None` seachas
`Some`, ní bheidh an patrún `Some(x)` comhoiriúnach.

Ní féidir le paraiméadair feidhme, ráitis `let`, agus lúba `for` ach patrúin neamh-inbhréagnaithe a ghlacadh, mar ní féidir leis an gclár aon rud bríoch a dhéanamh nuair nach
mbeidh luachanna ag teacht le chéile. Glacann na habairtí `if let` agus `while let` agus an ráiteas
`let`-`else` le patrúin inbhréagnaithe agus neamh-inbhréagnaithe, ach tugann an
comhléadaitheoir rabhadh i gcoinne patrúin neamh-inbhréagnaithe toisc go bhfuil siad de réir sainmhínithe
beartaithe chun déileáil le teip fhéideartha: tá feidhmiúlacht coinníollach ina
chumas feidhmiú ar bhealach difriúil ag brath ar rath nó teip.

Go ginearálta, níor cheart go mbeadh ort a bheith buartha faoin idirdhealú idir patrúin inbhréagnaithe
agus neamh-inbhréagnaithe; áfach, ní mór duit a bheith eolach ar choincheap
na hinbhréagnaitheachta ionas gur féidir leat freagairt nuair a fheiceann tú é i dteachtaireacht earráide. Sna
cásanna sin, beidh ort an patrún nó an tógáil a bhfuil tú ag
úsáid an phatrúin leis a athrú, ag brath ar an iompar atá beartaithe don chód.

Féachfaimid ar shampla de na rudaí a tharlaíonn nuair a dhéanaimid iarracht patrún inbhréagnaithe a úsáid
i gcás ina n-éilíonn Rust patrún neamh-inbhréagnaithe agus a mhalairt. Taispeánann Liostáil 19-8 ráiteas
`let`, ach don phatrún tá `Some(x)` sonraithe againn, patrún
inbhréagnaithe. Mar a bheifeá ag súil leis, ní thiomsófar an cód seo.

<Listing number="19-8" caption="Attempting to use a refutable pattern with `let`">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-08/src/main.rs:here}}
```

</Listing>

Dá mba luach `None` é `some_option_value`, theipfeadh air an patrún `Some(x)` a mheaitseáil, rud a chiallaíonn gur féidir an patrún a bhréagnú. Mar sin féin, ní féidir leis an ráiteas `let` glacadh le patrún dochloíte amháin mar níl aon rud bailí is féidir leis an gcód a dhéanamh le luach `None`. Ag am an tiomsaithe, gearánfaidh Rust gur thriail muid patrún dochloíte a úsáid nuair a bhíonn patrún dochloíte ag teastáil:

```console
{{#include ../../listings/ch19-patterns-and-matching/listing-19-08/output.txt}}
```

Ós rud é nár chlúdaíomar (agus nárbh fhéidir linn!) gach luach bailí a chlúdach leis an
patrún `Some(x)`, táirgeann Rust earráid tiomsaitheora go dlisteanach.

Má tá patrún inbhréagnaithe againn ina bhfuil gá le patrún dochloíte, is féidir linn
é a shocrú tríd an gcód a úsáideann an patrún a athrú: in ionad `let` a úsáid, is féidir linn `if let` a úsáid. Ansin mura n-oireann an patrún, scipeálfaidh an cód
an cód sna lúibíní casta, rud a thugann bealach dó leanúint ar aghaidh go bailí. Taispeánann Liostáil
19-9 conas an cód i Liostáil 19-8 a shocrú.

<Listing number="19-9" caption="Using `if let` and a block with refutable patterns instead of `let`">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-09/src/main.rs:here}}
```

</Listing>

Tá an cód curtha as againn! Tá an cód seo bailí go hiomlán anois. Mar sin féin, má thugaimid patrún dochloíte `if let` (patrún a bheidh i gcónaí ag teacht leis), amhail `x`, mar a thaispeántar i Liostáil 19-10, tabharfaidh an tiomsaitheoir rabhadh.

<Listing number="19-10" caption="Attempting to use an irrefutable pattern with `if let`">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-10/src/main.rs:here}}
```

</Listing>

Gearánann Rust nach bhfuil ciall le `if let` a úsáid le patrún dochloíte:

```console
{{#include ../../listings/ch19-patterns-and-matching/listing-19-10/output.txt}}
```

Ar an gcúis seo, ní mór do na hairm mheaitseála patrúin inbhréagnaithe a úsáid, seachas an lámh dheireanach, ar cheart di aon luachanna atá fágtha a mheaitseáil le patrún dochloíte. Ligeann Rust dúinn patrún dochloíte a úsáid i `match` le lámh amháin, ach
níl an comhréir seo thar a bheith úsáideach agus d'fhéadfaí ráiteas `let` níos simplí a athsholáthar.

Anois go bhfuil a fhios agat cá háit le patrúin a úsáid agus an difríocht idir patrúin inbhréagnaithe
agus dochloíte, déanaimis an comhréir go léir is féidir linn a úsáid chun patrúin
a chruthú a chlúdach.