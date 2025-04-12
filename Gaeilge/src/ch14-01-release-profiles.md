## Tógann Saincheapadh le Próifílí Eisiúna

I Rust, tá próifílí _release_ réamhshainithe agus próifílí inoiriúnaithe le
cumraíochtaí éagsúla a ligeann do ríomhchláraitheoir níos mó smachta a bheith acu
roghanna éagsúla chun cód a thiomsú. Tá gach próifíl cumraithe neamhspleách ar
na cinn eile.

Tá dhá phríomhphróifíl ag Cargo: an phróifíl `dev` a úsáideann Cargo nuair a ritheann tú `cargo
build` agus an phróifíl `release` a úsáideann Cargo nuair a ritheann tú `cargo build
--release`. Sainmhínítear an phróifíl `dev` le réamhshocruithe maithe le haghaidh forbartha,
agus tá mainneachtainí maithe ag an bpróifíl `release` maidir le tógáil scaoileadh.

Seans go bhfuil cur amach ar na hainmneacha próifíle seo ó aschur do chuid tógála:

<!-- athghiniúint de láimh
áit ar bith, rith:
tógáil lasta
lasta a thógáil --scaoileadh
agus a chinntiú go bhfuil an t-aschur thíos cruinn
-->

```console
$ cargo build
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.00s
$ cargo build --release
    Finished `release` profile [optimized] target(s) in 0.32s
```

Is iad na `dev` agus `release` na próifílí éagsúla seo a úsáideann an tiomsaitheoir.

Tá socruithe réamhshocraithe ag Cargo do gach ceann de na próifílí a bhíonn i bhfeidhm nuair nach bhfuil
cuireadh aon rannáin `[profile.*]` isteach go sainráite i gcomhad _Cargo.toml_ an tionscadail.
Trí rannáin `[profile.*]` a chur isteach d'aon phróifíl is mian leat a shaincheapadh, ní mór duit
aon fho-thacar de na socruithe réamhshocraithe a shárú. Mar shampla, anseo tá an réamhshocraithe
luachanna don socrú `opt-level` do na próifílí `dev` agus `release`:

<span class="filename">Ainm comhaid: Cargo.toml</span>

```toml
[profile.dev]
opt-level = 0

[profile.release]
opt-level = 3
```

Rialaíonn an socrú `opt-level` líon na n-uasmhéaduithe a mbainfidh Rust leo
do chód, le raon de 0 go 3. Síneann cur i bhfeidhm níos mó optimizations
am a thiomsú, mar sin má tá tú ag forbairt agus ag tiomsú do chód go minic,
beidh tú ag iarraidh níos lú optimizations a thiomsú níos tapúla fiú má tá an cód mar thoradh air
ritheann níos moille. Mar sin is é `0` an `opt-level` réamhshocraithe do `dev`. Nuair atá tú
réidh chun do chód a scaoileadh, is fearr níos mó ama a chaitheamh ag tiomsú. Beidh tú amháin
tiomsaigh i mód eisithe uair amháin, ach reáchtálfaidh tú an clár tiomsaithe go minic,
mar sin ceirdeanna modh scaoileadh níos faide ama a thiomsú le haghaidh cód a ritheann níos tapúla. Is é sin
cén fáth gurb é `3` an `opt-level` réamhshocraithe don phróifíl `release`.

Is féidir leat socrú réamhshocraithe a shárú trí luach difriúil a chur leis
_Cargo.toml_. Mar shampla, más mian linn leas iomlán a bhaint as leibhéal 1 sa
próifíl forbartha, is féidir linn an dá líne seo a chur le _Cargo.toml_ ár dtionscadal
comhad:

<span class="filename">Ainm comhaid: Cargo.toml</span>

```toml
[profile.dev]
opt-level = 1
```

Sáraíonn an cód seo an socrú réamhshocraithe `0`. Anois agus muid ag rith `cargo build`,
Úsáidfidh Cargo na réamhshocruithe don phróifíl `dev` móide ár n-oiriúnú do
`opt-level`. Toisc go bhfuil `opt-level` socraithe againn go `1`, beidh feidhm ag Cargo níos mó
optimizations ná an réamhshocrú, ach ní oiread agus is i scaoileadh scaoileadh.

Le haghaidh liosta iomlán na roghanna cumraíochta agus mainneachtainí do gach próifíl, féach
[Doiciméadú Cargo](https://doc.rust-lang.org/cargo/reference/profiles.html).