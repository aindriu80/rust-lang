## Comhad á Léamh

Anois cuirfimid feidhmiúlacht leis chun an comhad a shonraítear sa `file_path` a léamh
argóint. Ar dtús teastaíonn uainn comhad samplach chun é a thástáil: úsáidfimid comhad a bhfuil a
méid beag téacs thar línte iolracha le roinnt focal arís agus arís eile. Liostáil 12-3
Tá dán Emily Dickinson aige a oibreoidh go maith! Cruthaigh comhad darb ainm
_poem.txt_ ag bunleibhéal do thionscadal, agus cuir isteach an dán “Is Aon Duine mé!
Cé tusa?"

<Listing number="12-3" file-name="poem.txt" caption="A poem by Emily Dickinson makes a good test case.">

```text
{{#include ../../listings/ch12-an-io-project/listing-12-03/poem.txt}}
```

</Listing>

Agus an téacs i bhfeidhm, cuir _src/main.rs_ in eagar agus cuir cód leis chun an comhad a léamh, mar
léirithe i Liostú 12-4.

<Listing number="12-4" file-name="src/main.rs" caption="Reading the contents of the file specified by the second argument">

```rust,should_panic,noplayground
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-04/src/main.rs:here}}
```

</Listing>

Ar dtús tugaimid isteach cuid ábhartha den leabharlann chaighdeánach le `use`
ráiteas: ní mór dúinn `std::fs` chun comhaid a láimhseáil.

Sa `main`, glacann an ráiteas nua `fs::read_to_string` an `file_path`, osclaíonn sé
an comhad sin, agus seolann sé ar ais luach den chineál `std::io::Result<String>` ina bhfuil
inneachar an chomhaid.

Ina dhiaidh sin, cuirimid arís ráiteas sealadach `println!` a phriontálann an luach
de `contents` tar éis an comhad a léamh, ionas gur féidir linn a sheiceáil go bhfuil an clár
ag obair go dtí seo.

Rithfimid an cód seo le haon teaghrán mar an argóint chéad líne ordaithe (mar gheall ar
níl an chuid cuardaigh curtha i bhfeidhm againn fós) agus an comhad _poem.txt_ mar an
dara argóint:

```console
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-04/output.txt}}
```

Go hiontach! Léadh an cód agus ansin phriontáiltear ábhar an chomhaid. Ach an cód
tá cúpla lochtanna. I láthair na huaire, tá an fheidhm `main` iolraithe
freagrachtaí: go ginearálta, bíonn feidhmeanna níos soiléire agus níos éasca le cothabháil má
tá gach feidhm freagrach as smaoineamh amháin. Is í an fhadhb eile go bhfuil muid
gan earráidí a láimhseáil chomh maith agus a d'fhéadfaimis. Tá an clár fós beag, mar sin iad seo
ní fadhb mhór iad lochtanna, ach de réir mar a fhásann an clár, beidh sé níos deacra iad a shocrú
iad go glan. Is dea-chleachtas é tosú ar athmhachnamh go luath nuair
clár a fhorbairt mar go bhfuil sé i bhfad níos éasca méideanna níos lú a athfhachtóiriú
cód. Déanfaimid é sin chugainn.