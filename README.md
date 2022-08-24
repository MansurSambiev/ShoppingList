# ShoppingList
Создали EmptyActivity, разделили на три слоя (Domain, Data, Presentation), согласно CleanArchitecture.
Domain слой отвечает за бизнес логику приложения. Создаем Дата класс ShopList - элемент нашего списка, содержащий имя, количество, id и переменную, хранящую значение активности.
Создаем UseCase - каждый отвечает за одно-единственное действие:
Получение списка, создание, редактирование, удаление и получение отдельного элемента списка.
Создаем репозиторий со всеми функциями. Domain слой на этом завершен
Создаем Data слой. Создаем реализацию репозитория (почему object?), в котором переназначаем все функции.
Для хранения пока что используем коллекцию mutableList, для чего и создаем переменную для храннеия этого списка.
Добавление нового элемента будет записывать значение в список, удаление элемента удаляет значение из списка.
Полный список получаем возратом копии начального списка со свойством toList() чтобы нелья было редактировать исходный список.
Получение элемента списка реализуем с помощью свойства find по id элемента, прописываем исключение, чтобы приложение не выдало ошибку, если заданный элемент не найден.
Изменение элемента происходит как удаление старого элемента и добавление на его место нового, но так как новый элемент приходит нам в виде параметра,
мы не сможем его удалить, так как его нет в списке. Поэтому создаем переменную, добавляем в нее старый элемент по id, удаляем и добавляем новый элемент,
используя нашу функцию добавления.
У нас всплывает проблема, что нужно указывать уникальный id при создании нового объекта. Так как у нас не реализовано автоматическое присваивание id, устанавливаем
для переменной в дата классе значение по умолчанию (создаем константу UNDEFINED_ID со значением -1 в companion object (?)).
Создаем переменную в реализации репозитория для нового id и при создании каждого нового элемента увеличиваем это значение на единицу.
Но теперь нам при редактировании элемента нужно добавить его с таким же id - реализуем проверку при создании нового элемента совпадает ли он со значением id по умолчанию,
если Да - то присваиваем новый id, если нет, просто добавляем в список.
