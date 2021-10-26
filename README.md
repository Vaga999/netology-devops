 # Домашнее задание к занятию «2.4. Инструменты Git»
 ## 1. Найдите полный хеш и комментарий коммита, хеш которого начинается на aefea.
Для отображения списков коммитов вводим сначала :  
git log --oneline   
потом для поиска нужного коммита:  
git show aefea
где aefea сокращеный хэш искомого коммита  

commit aefead2207ef7e2aa5dc81a34aedf0cad4c32545
Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>
Date:   Thu Jun 18 10:29:58 2020 -0400

## 2. Какому тегу соответствует коммит 85024d3?
Вводим:  
git show 85024d3  
где  85024d3 это сокращенный хэш искомого коммита.
Получаемый вывод:  
commit 85024d3100126de36331c6982bfaac02cdab9e76 (tag: v0.12.23)
Author: tf-release-bot <terraform@hashicorp.com>
Date:   Thu Mar 5 20:56:10 2020 +0000
Нужный тэг  v0.12.23

## 3. Сколько родителей у коммита b8d720? Напишите их хеши.
Вводим $ git show --format=%p b8d720  
Вывод хэши родителей, здесь количество родителей = 2:  
56cd7859e 9ea88f22f
%p – показывает только родителей.  

## 4. Перечислите хеши и комментарии всех коммитов, которые были сделаны между тегами v0.12.23 и v0.12.24.  
Вводим:  
$ git log v0.12.23..v0.12.24  
В выводе получаем список коммитов между тэгами.  
Список хэшей и коментариев к ним:  

commit 33ff1c03bb960b332be3af2e333462dde88b279e (tag: v0.12.24)
Author: tf-release-bot <terraform@hashicorp.com>
Date:   Thu Mar 19 15:04:05 2020 +0000

    v0.12.24

commit b14b74c4939dcab573326f4e3ee2a62e23e12f89
Author: Chris Griggs <cgriggs@hashicorp.com>
Date:   Tue Mar 10 08:59:20 2020 -0700

    [Website] vmc provider links

commit 3f235065b9347a758efadc92295b540ee0a5e26e
Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>
Date:   Thu Mar 19 10:39:31 2020 -0400

    Update CHANGELOG.md

commit 6ae64e247b332925b872447e9ce869657281c2bf
Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>
Date:   Thu Mar 19 10:20:10 2020 -0400

    registry: Fix panic when server is unreachable

    Non-HTTP errors previously resulted in a panic due to dereferencing the
    resp pointer while it was nil, as part of rendering the error message.
    This commit changes the error message formatting to cope with a nil
    response, and extends test coverage.

    Fixes #24384

commit 5c619ca1baf2e21a155fcdb4c264cc9e24a2a353
Author: Nick Fagerlund <nick.fagerlund@gmail.com>
Date:   Wed Mar 18 12:30:20 2020 -0700

    website: Remove links to the getting started guide's old location

    Since these links were in the soon-to-be-deprecated 0.11 language section, I
    think we can just remove them without needing to find an equivalent link.

commit 06275647e2b53d97d4f0a19a0fec11f6d69820b5
Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>
Date:   Wed Mar 18 10:57:06 2020 -0400

    Update CHANGELOG.md

commit d5f9411f5108260320064349b757f55c09bc4b80
Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>
Date:   Tue Mar 17 13:21:35 2020 -0400

    command: Fix bug when using terraform login on Windows

commit 4b6d06cc5dcb78af637bbb19c198faff37a066ed
Author: Pam Selle <pam@hashicorp.com>
Date:   Tue Mar 10 12:04:50 2020 -0400

    Update CHANGELOG.md

commit dd01a35078f040ca984cdd349f18d0b67e486c35
Author: Kristin Laemmert <mildwonkey@users.noreply.github.com>
Date:   Thu Mar 5 16:32:43 2020 -0500

    Update CHANGELOG.md

commit 225466bc3e5f35baa5d07197bbc079345b77525e
Author: tf-release-bot <terraform@hashicorp.com>
Date:   Thu Mar 5 21:12:06 2020 +0000

    Cleanup after v0.12.23 release


## 5. Найдите коммит в котором была создана функция func providerSource, ее определение в коде выглядит так func providerSource(...) (вместо троеточего перечислены аргументы).  
Вводим:  
git log -S 'func providerSource' --oneline  
Вывод :  
5af1e6234 main: Honor explicit provider_installation CLI config when present  
8c928e835 main: Consult local directories as potential mirrors of providers  

Можно посмотреть сами коммиты :  
git show 5af1e6234  
git show 8c928e835  

Этот коммит 8c928e835 самый ранний из списка, соответственно в нем и появилась функция.

## 6. Найдите все коммиты в которых была изменена функция globalPluginDirs.  
Сначала ищем то где появился globalPluginDirs:  
git log -S 'globalPluginDirs' –oneline

Получаем:  
35a058fb3 main: configure credentials from the CLI config file  
c0b176109 prevent log output during init  
8364383c3 Push plug  
Здесь 35a058fb3 самый ранний, смотрим его видим что если сделать поиск globalPluginDirs , то фукнкция находится в файле plugins.go  

Дальше   
git log -L :'globalPluginDirs':plugins.go --oneline  
Получим список коммитов где велась работа с функцией:  
78b122055  
52dbf9483  
41ab0aef7  


## 7. Кто автор функции synchronizedWriters?  
Вводим:  
git log -S 'synchronizedWriters' --pretty=format:"%H %ad %an"  

bdfea50cc85161dea41be0fe3381fd98731ff786 Mon Nov 30 18:02:04 2020 -0500 James Bardin  
fd4f7eb0b935e5a838810564fd549afe710ae19a Wed Oct 21 13:06:23 2020 -0400 James Bardin  
5ac311e2a91e381e2f52234668b49ba670aa0fe5 Wed May 3 16:25:41 2017 -0700 Martin Atkins  
Судя по дате самое раннее упоминание 2017 год Martin Atkins
