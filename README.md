# Списки заблокированных ресурсов
Списки доступны в нескольких форматах:
- RAW - это список доменов и субдоменов
- Dnsmasq-ipset - список для Dnsmasq в формате ipset (OpenWrt <= 21.02)
- Dnsmasq-nfset - список для Dnsmasq в формате nftables set (OpenWrt >=22.03).

Конфигурация для Dnsmasq добавляет все зарезолвенные IP-адреса в set `vpn-domain`. И можно оперировать этим списком.

## Россия

- Ресурсы, которые блокирует провайдеры по наводке РКН, и зарубежные ресурсы, которые сами блокируют российские подсети. (inside)

Находятся в каталоге **Russia**.

Inside:
- [RAW](https://raw.githubusercontent.com/gitbatoff/first/main/Russia/inside-raw.lst)
- [Dnsmasq nfset](https://raw.githubusercontent.com/gitbatoff/first/main/Russia/inside-dnsmasq-nfset.lst)
- [Dnsmasq ipset](https://raw.githubusercontent.com/gitbatoff/first/main/Russia/inside-dnsmasq-ipset.lst)
- [ClashX](https://raw.githubusercontent.com/gitbatoff/first/main/Russia/inside-clashx.lst)


# Как добавить домены в списки?

Сделать PR. Списки находятся в `src`. Если у ресурса больше двух доменов, сгруппируйте их отдельным списком и вставьте заголовок ресурса с помощью `#`. Ориентируйтесь на то, как уже сделаны другие

# Как устроено?
Список **Russia inside** формируются из списка https://community.antifilter.download/ и списка `src/Russia-domains-inside.lst`. Они объединяются, удаляются повторы и сортируются по алфавиту. 

Dnmasq работает по wildcard. Это означает, что при добавлении домена `domain.com`, в списки IP-адресов будут добавляться также все поддомены `subdomain.domain.com`. Поэтому Dnsmasq списки состоят только из доменов второго уровня. Повторы удаляются, удаляются субдомены с `google.com` и происходит сортировка.

Списки обновляются при каждом коммите в репозитории с помощью GitHub Actions. Также скрипт `convert.py` запускается каждые 8 часов, чтобы синхронизировать списки со сторонними сервисами.

При формировании Dnsmasq списков происходит тестирование конфигов с помощью [Dnsmasq action](https://github.com/marketplace/actions/dnsmasq-configuration-check).

# first

