Списки:
- RAW - это список доменов и субдоменов
- Dnsmasq-nfset - список для Dnsmasq в формате nftables set (OpenWrt >=22.03).

Конфигурация для Dnsmasq добавляет все зарезолвенные IP-адреса в set `vpn-domain`. И можно оперировать этим списком.

- [RAW](https://raw.githubusercontent.com/gitbatoff/first/main/Russia/inside-raw.lst)
- [Dnsmasq nfset](https://raw.githubusercontent.com/gitbatoff/first/main/Russia/inside-dnsmasq-nfset.lst)
- [Dnsmasq ipset](https://raw.githubusercontent.com/gitbatoff/first/main/Russia/inside-dnsmasq-ipset.lst)
- [ClashX](https://raw.githubusercontent.com/gitbatoff/first/main/Russia/inside-clashx.lst)

Как добавить домены в списки?

Списки находятся в `src`. Если у ресурса больше двух доменов, сгруппируйте их отдельным списком и вставьте заголовок ресурса с помощью `#`. Ориентируйтесь на то, как уже сделаны другие

Как устроено?
Список формируются из списка https://community.antifilter.download/ и списка `src/Russia-domains-inside.lst`. Они объединяются, удаляются повторы и сортируются по алфавиту. 

Dnmasq работает по wildcard. Это означает, что при добавлении домена `domain.com`, в списки IP-адресов будут добавляться также все поддомены `subdomain.domain.com`. Поэтому Dnsmasq списки состоят только из доменов второго уровня. Повторы удаляются, удаляются субдомены с `google.com` и происходит сортировка.

Списки обновляются скриптом `convert.py` и запускается каждые 8 часов, чтобы синхронизировать списки с https://community.antifilter.download/

# first

