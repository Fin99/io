# Лабораторная работа 1

**Название:** "Разработка драйверов символьных устройств"

**Цель работы:** Получить знания и навыки разработки драйверов символьных устройств для операционной системы Linux.

## Описание функциональности драйвера

При записи текста в файл символьного устройства должно запоминаться количество введенных символов. Последовательность полученных результатов с момента загрузки модуля ядра должна выводиться при чтении созданного файла `/proc/var1` в консоль пользователя.

При чтении из файла символьного устройства в кольцевой буфер ядра должен осуществляться вывод тех же данных, которые выводятся при чтении файла `/proc/var1`.


## Инструкция по сборке

Для сборки необходимо запустить комманду:

```
make
```

## Инструкция пользователя

Для загрузки драйвера необходимо запустить комманду:

```
sudo insmod char.ko
```

Чтобы иметь доступ к записи в символьное устройство `var1`, нужно сделать одно из двух:

- Получить права суперпользователя: `sudo su -`

Для записи данных в символьное устройство необходимо использовать комманду:

```
echo "data" > /dev/var1
```

Для чтения `proc`-файла:

```
cat /proc/var1
```

Для чтения символьного устройства:

```
cat /dev/var1
```

Для проверки кольцевого буфера:

```
dmesg
```

Для выгрузки драйвера:

```bash
sudo rmmod char
```

## Примеры использования

Запись данных в символьное устройство и чтение результата из файла `/proc/var1`:

```bash
sudo insmod char.ko; 
echo > /dev/var1 
echo "1" > /dev/var1 
echo "123a" > /dev/var1 
cat /proc/var1 
1 - 0
2 - 1
3 - 4

```

Запись данных в символьное устройство и чтение результата из кольцевого буфера:

```bash
sudo insmod char.ko; 
echo > /dev/var1 
echo "1" > /dev/var1 
echo "123a" > /dev/var1 
cat /dev/mychdev
dmesg
...
[ 2273.089620] Hello!
[ 2503.070840] 1 - 0
[ 2503.070844] 2 - 1
[ 2503.070845] 3 - 4
```
