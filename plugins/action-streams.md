# Action Streams

''Этот тег доступен только при наличии [[Плагин Action Streams|плагина Action Streams]], который есть в стандартном дистрибутиве Movable Type 4.25 и выше.''

== Пример ==

Этот блок с тегами шаблонов показывает, как отобразить на сайте последние действия пользователей, которые они совершили в профилях, указанных в Action Streams.

<source lang="html4strict">
<mt:ActionStreams>
    <mt:DateHeader>
        <div>
            <h3><$mt:StreamActionDate format="%b %d, %Y"$></h3>
            <ul>
    </mt:DateHeader>
                <li class="service-<$mt:var name="service_type"$>">
                    <mt:StreamActionDate format="%H:%M"> - <$MTStreamAction$>
                </li>
    <mt:DateFooter>
            </ul>
        </div>
    </mt:DateFooter>
</mt:ActionStreams>
</source>


== Атрибуты ==

* '''author''' (опционально) 
Ограничивает отображение действий одним конкретным пользователем.Используйте в этом атрибуте имя пользователя (username).

Например, если вы хотите отобразить действия пользователя «Melody»:
<source lang="xml"><mt:ActionStreams author="Melody"></source>

Чтобы отобразить действия нескольких пользователей, необходимо разделить их имена запятыми:
<source lang="xml"><mt:ActionStreams author="Melody,Serge"></source>


* '''display_name''' (опционально) 
Тоже самое, что атрибут author. Только вместо имени пользователя необходимо указывать отображаемое имя.

Например, чтобы отобразить действия пользователя, у которого отображаемое имя — «Melody Nelson»:
<source lang="xml"><mt:ActionStreams display_name="Melody"></source>

Чтобы отобразить действия нескольких пользователей, необходимо разделить их отображаемые имена запятыми:
<source lang="xml"><mt:ActionStreams display_name="Melody Nelson, Serge Gainsbourg"></source>


* '''author_id''' (опционально) 
Тоже самое, что author и display_name. Но вместо имён в этом атрибуте необходимо указывать ID пользователя.

Например, чтобы отобразить действия пользователя, у которого ID — 3:
<source lang="xml"><mt:ActionStreams author_id="3"></source>

Чтобы отобразить действия нескольких пользователей, разделите их ID запятыми:
<source lang="xml"><mt:ActionStreams author_id="3,4,7"></source>

Только один из атрибутов author_id display_name и author может быть использован одновременно. Если ни один их этих атрибутов не указан, то отображение действий происходит в зависимости от контекста: если тег используется в контексте автора (например, на странице архива автора, внутри [[Authors|<mt:Authors>]] тега, в контексте записи или на странице профиля пользователя), то будут показаны действия одного автора; в противном случае, если тег используется в контексте блога, то будут показаны действия всех авторов, которые имеют доступ к этому блогу.


* '''limit''' (опционально) 
Максимальное количество действий, которые будут показаны. Если действий меньше указанного числа, то будет отображено меньшее количество.


* '''days''' (опционально) 
Ограничение вывода действий временным отрезком. Будут отображены только записи за указанное количество дней.
<source lang="xml"><mt:ActionStreams days="10"></source>

Может быть использован либо days, либо limit. Если ничего не указано, то будут отображены последние 20 действий.


* '''service''' (опционально) 
Идентификатор сервиса, действия с которого будут отображены. Идентификатор сервиса отличается от его написания. Например, идентификатор сервиса Twitter — twitter, а Delicious — delicious.

Если сервис содержит несколько потоков, ограничение атрибутом service без атрибута stream, выведет все потоки этого сервиса.Например, при указании service="flickr" будут отображены добавленные фотографии на Flickr, а также избранное на Flickr.
<source lang="xml">
<mt:ActionStreams service="flickr">
    <!-- Фотографии с Flickr, избранное оттуда и т.д. -->
</mt:ActionStreams>
</source>


* '''stream''' (опционально) 
Идентификатор потока, который будет отображён. Идентификатор потока — это определённые ключи, используемые для разграничения нескольких потоков в рамках одного сервиса. Например, поток ссылок Delicious имеет идентификатор links, а поток фотографий Flickr — photos.

Поскольку разные сервисы могут использовать одни и те же названия для потоков, вы можете использовать идентификатор потока в атрибуте stream, что в результате приведёт к отображению всех действий с этим идентификатором с различных сервисов.Например, вы можете указать stream="photos", без указания атрибута service, чтобы отобразить все действия с фото, или stream="favorites" для отобразить избранное.

<source lang="xml">
<mt:ActionStreams stream="photos">
    <!-- Фотографии со всех сервисов -->
</mt:ActionStreams>
</source>

Чтобы получить список определённых действий с одного конкретного сервиса можно использовать атрибуты service и stream.
<source lang="xml">
<mt:ActionStreams service="flickr" stream="favorites">
    <!-- Только избранное с Flickr -->
</mt:ActionStreams>
</source>


* '''sort_by''' (опционально) 
Определяет поле, по которому будут сортироваться действия. По умолчанию действия сортируются по полю created_on (то есть времени, когда действие произошло или было впервые получено).
Доступные поля для сортировки:
# author_id — числовой идентификатор автора;
# created_on — дата и время, когда действие произошло или было впервые получено;
# modified_on — дата и время, когда действие было в последний раз изменено.


* '''direction''' (опционально)
Определяет порядок, по которому сортируются действия. Возможные значения:
# descend — самое новое вверху, самое старое внизу);
# ascend — самое старое вверху, самое новое внизу).
По умолчанию действия отсортированы по порядку descend.

<source lang="xml">
<mt:ActionStreams sort_by="author_id" direction="ascend">
    <!-- Действия остортированы по ID автора, самое старое вверху -->
</mt:ActionStreams>
</source>

[[Категория:Теги шаблонов]]
[[Категория:Избранные статьи]]
