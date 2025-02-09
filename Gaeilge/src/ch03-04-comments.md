## Tuairimí

Déanann gach ríomhchláraitheoir a ndícheall a gcód a dhéanamh éasca le tuiscint, ach uaireanta
tá míniú breise ag teastáil. Sna cásanna seo, fágann ríomhchláraitheoirí _comments_ isteach
a gcód foinse nach ndéanfaidh an tiomsaitheoir neamhaird air ach daoine ag léamh na foinse
d'fhéadfadh go mbeadh cód úsáideach.

Seo trácht simplí:

```rust
// hello, world
```

I Rust, cuireann an stíl tráchtaireacht idiotach tús le trácht le dhá slais, agus an
leanann trácht ar aghaidh go dtí deireadh na líne. Le haghaidh tuairimí a théann thar a
líne shingil, beidh ort `//` a chur san áireamh ar gach líne, mar seo:

```rust
// Mar sin táimid ag déanamh rud casta anseo, fada go leor agus a theastaíonn uainn
// línte iolracha de thuairimí chun é a dhéanamh! Whew! Tá súil agam go ndéanfaidh an trácht seo
// mínigh cad atá ar siúl.
```

Is féidir tuairimí a chur freisin ag deireadh línte ina bhfuil cód:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-24-comments-end-of-line/src/main.rs}}
```

Ach feicfidh tú níos minice iad a úsáid san fhormáid seo, leis an trácht ar a
líne ar leith os cionn an chóid atá á nótáil aige:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-25-comments-above-line/src/main.rs}}
```

Tá trácht de chineál eile ag Rust freisin, tuairimí doiciméadaithe, a dhéanfaimid
pléigh san [“Cliathbhosca a Fhoilsiú go cliathbhoscaí.io”][publishing]<!-- ignore -->
alt de Chaibidil 14.

[publishing]: ch14-02-publishing-to-crates-io.html