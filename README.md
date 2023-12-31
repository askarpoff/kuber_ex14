# Домашнее задание к занятию «Обновление приложений»

### Цель задания

Выбрать и настроить стратегию обновления приложения.

-----

### Задание 1. Выбрать стратегию обновления приложения и описать ваш выбор

1. Имеется приложение, состоящее из нескольких реплик, которое требуется обновить.
2. Ресурсы, выделенные для приложения, ограничены, и нет возможности их увеличить.
3. Запас по ресурсам в менее загруженный момент времени составляет 20%.
4. Обновление мажорное, новые версии приложения не умеют работать со старыми.
5. Вам нужно объяснить свой выбор стратегии обновления приложения.

### Задание 2. Обновить приложение

1. Создать deployment приложения с контейнерами nginx и multitool. Версию nginx взять 1.19. Количество реплик — 5.
2. Обновить версию nginx в приложении до версии 1.20, сократив время обновления до минимума. Приложение должно быть доступно.
3. Попытаться обновить nginx до версии 1.28, приложение должно оставаться доступным.
4. Откатиться после неудачного обновления.

### Ответ:

### Задание 1. Выбрать стратегию обновления приложения и описать ваш выбор

Можно было бы попробовать использовать стратегию __Rolling Update__ и обновлять по одной реплике за раз, экономя ресурсы, но тогда возможны проблемы из-за мажорного обновления.

Таким образом, чтобы всем условиям удовлетрворяло, взять __Recreate__ - предупредить о недоступности во время минимальной нагрузки, грохнуть старые версии одномоментно, задеплоить новые на их месте - нет необходимости увеличивать расход ресурсов, нет влияния версий.

### Задание 2. Обновить приложение

1. Создать deployment приложения с контейнерами nginx и multitool. Версию nginx взять 1.19. Количество реплик — 5.

[deployment.yaml](https://github.com/askarpoff/kuber_ex14/blob/main/manifest/deployment.yaml)

![image](https://github.com/askarpoff/kuber_ex14/assets/108946489/e648b8c3-4e0d-4c2e-9943-91d0e4f51876)

2. Обновить версию nginx в приложении до версии 1.20, сократив время обновления до минимума. Приложение должно быть доступно.

![image](https://github.com/askarpoff/kuber_ex14/assets/108946489/4fe69f31-cd9d-4ad0-9c14-79277d6e71fd)
![image](https://github.com/askarpoff/kuber_ex14/assets/108946489/1d5c7fb4-0b6d-4fd5-a088-b1a580bffeae)

3. Попытаться обновить nginx до версии 1.28, приложение должно оставаться доступным.

![image](https://github.com/askarpoff/kuber_ex14/assets/108946489/ca143416-81ad-418e-8111-728fbc26e900)

4. Откатиться после неудачного обновления.

Делаю ```kubectl rollout undo deployment app --to-revision=2```
![image](https://github.com/askarpoff/kuber_ex14/assets/108946489/fe7eafc6-62e7-4d4b-a171-c6d03fe3f9fd)
