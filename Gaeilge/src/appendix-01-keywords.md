## Aguisín A: Eochairfhocail

Tá eochairfhocail sa liosta seo a leanas atá curtha in áirithe le haghaidh úsáide reatha nó úsáide amach anseo ag an teanga Rust. Dá bhrí sin, ní féidir iad a úsáid mar aitheantóirí (seachas
mar aitheantóirí amha mar a phléifimid sa chuid “[Aitheantóirí Amha][aitheantóirí-amh]<!-- neamhaird a dhéanamh -->”). Is ainmneacha
feidhmeanna, athróg, paraiméadair, réimsí struchtúr, modúl, cliathbhoscaí, tairiseacha,
macra, luachanna statach, tréithe, cineálacha, tréithe, nó saolréanna iad aitheantóirí.

[amh-aitheantóirí]: #amh-aitheantóirí

### Eochairfhocail atá in Úsáid faoi Láthair

Seo a leanas liosta d'eochairfhocail atá in úsáid faoi láthair, agus a bhfeidhmiúlacht
cur síos orthu.

- `as` - réitigh phrimitiúla a dhéanamh, an tréith shonrach ina bhfuil mír a dhí-athbhriú, nó míreanna a athainmniú i ráitis `use`
- `async` - `Future` a thabhairt ar ais in ionad an snáithe reatha a bhlocáil
- `await` - forghníomhú a chur ar fionraí go dtí go mbeidh toradh `Future` réidh
- `break` - lúb a scoir láithreach
- `const` - míreanna tairiseacha nó pointeoirí amha tairiseacha a shainiú
- `continue` - leanúint ar aghaidh go dtí an chéad athrá lúb eile
- `crate` - i gcosán modúil, tagraíonn sé don fhréamh cliathbhosca
- `dyn` - seolta dinimiciúil chuig réad tréithe
- `else` - cúltaca do `if` agus `if let` tógálacha sreabhadh rialaithe
- `enum` - áireamh a shainiú
- `extern` - feidhm nó athróg sheachtrach a nascadh
- `false` - Litriúil bréagach Booleanach
- `fn` - feidhm nó an cineál pointeora feidhme a shainiú
- `for` - lúb a chur thar mhíreanna ó athrá, tréith a chur i bhfeidhm, nó saolré níos airde a shonrú
- `if` - brainse bunaithe ar toradh ar shliocht coinníollach
- `impl` - feidhmiúlacht dhúchasach nó tréith a chur i bhfeidhm
- `in` - cuid de chomhréir lúb `for`
- `let` - athróg a cheangal
- `loop` - lúbadh gan choinníoll
- `match` - luach a mheaitseáil le patrúin
- `mod` - modúl a shainiú
- `move` - dúnadh a dhéanamh chun úinéireacht a ghlacadh ar a ghabhálacha go léir
- `mut` - inathraitheacht a léiriú i dtagairtí, pointeoirí amha, nó ceangail patrún
- `pub` - infheictheacht phoiblí a léiriú i réimsí struchtúr, bloic `impl`, nó modúil
- `ref` - ceangal trí thagairt
- `return` - filleadh ó fheidhm
- `Self` - leasainm cineáil don chineál atá á shainiú nó á chur i bhfeidhm againn
- `self` - ábhar modha nó modúl reatha
- `static` - athróg dhomhanda nó saolré a mhaireann ar feadh fhorghníomhú iomlán an chláir
- `struct` - struchtúr a shainiú
- `super` - modúl tuismitheora an mhodúil reatha
- `trait` - tréith a shainiú
- `true` - fíor-litriúil Booleanach
- `type` - leasainm cineáil nó gaolmhar a shainiú cineál
- `aontas` - sainmhínigh [aontas][union]<!-- neamhaird a dhéanamh -->; ní eochairfhocal é ach nuair a úsáidtear é i ndearbhú aontas
- `neamhsábháilte` - cuir cód, feidhmeanna, tréithe nó cur i bhfeidhm neamhshábháilte in iúl
- `úsáid` - tabhair siombailí isteach sa raon feidhme; sonraigh gabhálacha beachta le haghaidh teorainneacha cineálacha agus saoil
- `cá háit` - cuir clásail in iúl a chuireann srian ar chineál
- `cé go` - lúb bunaithe go coinníollach ar thoradh na habairte

<!--[union]: ../reference/items/unions.html --> 
[union]: https://doc.rust-lang.org/stable/reference/items/unions.html

### Eochairfhocail atá curtha in áirithe le húsáid sa todhchaí

Níl aon fheidhmiúlacht ag na heochairfhocail seo a leanas go fóill ach tá siad curtha in áirithe ag
Rust le húsáid amach anseo.

- `abstract`
- `become`
- `box`
- `do`
- `final`
- `gen`
- `macro`
- `override`
- `priv`
- `try`
- `typeof`
- `unsized`
- `virtual`
- `yield`



### Aitheantóirí Amha

Is iad _Raw Identifiers_ an comhréir a ligeann duit eochairfhocail a úsáid i gcás nach mbeadh siad ceadaithe de ghnáth. Úsáideann tú aitheantóir amh trí réimír `r#` a chur le heochairfhocal.

Mar shampla, is eochairfhocal é `match`. Má dhéanann tú iarracht an fheidhm seo a leanas a thiomsú
a úsáideann `match` mar ainm:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust,ignore,does_not_compile
fn match(needle: &str, haystack: &str) -> bool {
    haystack.contains(needle)
}
```

gheobhaidh tú an earráid seo:

```text
error: expected identifier, found keyword `match`
 --> src/main.rs:4:4
  |
4 | fn match(needle: &str, haystack: &str) -> bool {
  |    ^^^^^ expected identifier, found keyword
```

Léiríonn an earráid nach féidir leat an eochairfhocal `match` a úsáid mar aitheantóir feidhme. Chun `match` a úsáid mar ainm feidhme, ní mór duit comhréir amh an aitheantóra a úsáid, mar seo:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
fn r#match(needle: &str, haystack: &str) -> bool {
    haystack.contains(needle)
}

fn main() {
    assert!(r#match("foo", "foobar"));
}
```

Tiomsóidh an cód seo gan aon earráidí. Tabhair faoi deara an réimír `r#` ar ainm na feidhme ina sainmhíniú chomh maith leis an áit a nglaotar ar an bhfeidhm i `main`.

Ligeann aitheantóirí amha duit aon fhocal a roghnaíonn tú a úsáid mar aitheantóir, fiú má
thiteann an focal sin mar eochairfhocal forchoimeádta. Tugann sé seo níos mó saoirse dúinn ainmneacha aitheantóirí a roghnú, chomh maith le ligeann sé dúinn comhtháthú le cláir atá scríofa i
dteanga nach eochairfhocail iad na focail seo. Ina theannta sin, ligeann aitheantóirí amha duit leabharlanna atá scríofa in eagrán Rust difriúil a úsáid ná mar a úsáideann do chliathán.
Mar shampla, ní eochairfhocal é `try` san eagrán 2015 ach tá sé sna heagráin 2018, 2021,
agus 2024. Má bhraitheann tú ar leabharlann atá scríofa ag baint úsáide as eagrán 2015
agus a bhfuil feidhm `try` aici, beidh ort comhréir an aitheantóra amh,
`r#try` sa chás seo, a úsáid chun an fheidhm sin a ghlaoch ó do chód eagrán 2018. Féach
[Aguisín E][appendix-e]<!-- neamhaird a dhéanamh --> le haghaidh tuilleadh eolais faoi eagráin.

[appendix-e]: appendix-05-editions.html
