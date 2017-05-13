# AniDub-CommentFinder
Provide interface for find comment: from the top on anime page, from user's last comments list. Provide api too.

Скрипт (userscript) предназначен для поиска комментов на сайте online.anidub.com.
Предоставляет интерфейс для поиска комментов из топа для страниц показа тайтла и листа последних комментариев пользователя, а также api для организации собственных скриптов на основе этого.
Использован api самого online.anidub.com.

# Использование
1. Для поиска комментариев из топа нужно:
  + перейти на страницу с аниме, на которой искомые комменты расположены
  + спуститься к топу и нажать на кнопку "ИСКАТЬ?".
  Если поиск удачен, то клик на любом комменте топа приводит к перелистыванию комментов на страницу с этим комментарием.

2. Для поиска комментов из листа последних у любого пользователя нужно:
  + Перейти в профиль нужного пользователя
  + После чего в раздел "Последние комментарии "
  + Выбрать коммент из списка
  + Для выбранного коммента нажать кнопку "НАЙТИ" (под аватаркой).
  Это откроет страницу с тайтлом, под которым расположен коммент и производит поиск. По окончании комментарии перелистнуться автоматически. Повторное нажатие открывает нужный коммент уже без поиска.

# API

**window.ad_searchManager(arg)** - принимает строку или массив строк. Результат её работы – промис, который, в случае удачного выполнения, возвращает массив номеров страниц (page), на которых расположены комментарии, в том порядке, в котором были переданы id искомых комментов. Если один из номеров равен -1, значит, комментарий с id под этим индексом не был найден. Вызванная без параметров, начинает искать комментарии топа
**window.ad_getCommentsList(page, news_id)** - принимает номер листа с комментариями и id страницы показа. Результат её работы - промис, который, в случае удачного выполенния, возвращает полученные данные. Используется в window.ad_showComment()
**window.ad_showComment(page, news_id[, comm_id])** - принимает номер листа с комментариями, id страницы показа и - необязательный параметр - id комментария. Если не указан comm_id, почти аналогична commentPage стандартного api. При вызове с comm_id, автоматически переводит искомый комментарий в видимую область
**"ad_finderonload"**  событие объекта window, срабатывающее при окончании загрузки скрипта
**"ad_oncommentdraw"** - событие объекта window, срабатывающее при окончании работы window.ad_showComment
