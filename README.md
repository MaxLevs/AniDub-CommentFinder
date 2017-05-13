# AniDub-CommentFinder
Provide interface for find comment: from the top on anime page, from user's last comments list. Provide api too.

Скрипт (userscript) предназначен для поиска комментов на сайте __online.anidub.com__.
Предоставляет интерфейс для поиска комментов из топа для страниц показа тайтла и листа последних комментариев пользователя, а также api для организации собственных скриптов на основе этого.
Использован api самого online.anidub.com.

# Использование
1. Для поиска комментариев из __топа__ нужно:
    + перейти на страницу с аниме, на которой искомые комменты расположены
    + спуститься к топу и нажать на кнопку "__ИСКАТЬ?__".
  Если поиск удачен, то клик на _любом комменте топа_ приводит к перелистыванию комментов на страницу с этим комментарием.

2. Для поиска комментов из __листа последних__ у любого пользователя нужно:
    + Перейти __в профиль__ нужного пользователя
    + После чего в раздел "__Последние комментарии__"
    + Выбрать коммент из списка
    + Для выбранного коммента нажать кнопку "__НАЙТИ__" (под аватаркой).
  Это откроет страницу с тайтлом, под которым расположен коммент и производит поиск. По окончании комментарии перелистнуться автоматически. Повторное нажатие открывает нужный коммент уже без поиска.

__ВНИМАНИЕ!! (о втором способе)__ Если вкладка с тайтлом _уже открыта_, и следующий коммент находятся под _тем же_ тайтлом, то новая страница, рядом с уже имеющейся, открыта __не будет__. Вместо этого поиск начнется _на уже открытой_ вкладке, на которой отобразиться уже _новый результат поиска_. Это нормальная работа скрипта, так и задумано. Если это будет доставлять неудобства, пишите либо на [форум](http://forum.anidub.com/topic/12898-%D0%BF%D1%80%D0%B5%D0%B4%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BA%D0%BB%D0%B8%D0%BA%D0%B0%D0%B1%D0%B5%D0%BB%D1%8C%D0%BD%D1%8B%D0%B5-%D0%BA%D0%BE%D0%BC%D0%BC%D0%B5%D0%BD%D1%82%D0%B0%D1%80%D0%B8%D0%B8-%D0%B8%D0%B7-%D1%82%D0%BE%D0%BF%D0%B0/ 'Кликабельные комментарии из топа'), либо на [github](https://github.com/MaxLevs/AniDub-CommentFinder/issues 'Issues') – реализую по-другому.

# API

**`window.ad_searchManager(arg)`** - принимает строку или массив строк. Результат её работы – промис, который, в случае удачного выполнения, возвращает массив номеров страниц (page), на которых расположены комментарии, в том порядке, в котором были переданы id искомых комментов. Если один из номеров равен -1, значит, комментарий с id под этим индексом не был найден. Вызванная без параметров, начинает искать комментарии топа

**`window.ad_getCommentsList(page, news_id)`** - принимает номер листа с комментариями и id страницы показа. Результат её работы - промис, который, в случае удачного выполенния, возвращает полученные данные. Используется в window.ad_showComment()

**`window.ad_showComment(page, news_id[, comm_id])`** - принимает номер листа с комментариями, id страницы показа и - необязательный параметр - id комментария. Если не указан comm_id, почти аналогична commentPage стандартного api. При вызове с comm_id, автоматически переводит искомый комментарий в видимую область

**"ad_finderonload"** - событие объекта window, срабатывающее при окончании загрузки скрипта

**"ad_oncommentdraw"** - событие объекта window, срабатывающее при окончании работы window.ad_showComment
