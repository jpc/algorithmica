---
title: Корневые эвристики
---

Иногда в задаче возникают ситуации, когда мы умеем решать ее когда
какое-то свойство \< $\\sqrt{N}$ и больше $\\sqrt{N}$. Данный
подход и называется корневой декомпозицией(оптимизацией).

Самыми простыми и наиболее известными применениями данной оптимизации
являются : алгоритм проверки на простоту чисел(рассмотрим делители \<
$\\sqrt{N}$ и больше, но так как для любого делителя больше корня можно
найти делитель меньше корня =\> нам надо честно рассмотреть только
первые) и например факт, что если суммарная длина строк = $N$, то
различных длин строк будет не более $\\sqrt{N}$ или если вы увидели
ограничение $A \* B \<= N$, то одно из чисел \< $\\sqrt{N}$.

Данные идеи очень полезны в задачах, где есть ограничение на суммарный
размер строк. Обозначим это ограничение за $\\sum |S|$.

#### Разбиение на длинные и короткие строки

Назовем строку $S \\ \\textit{длинной}$, если $|S| \\ge \\sqrt{\\sum
|S|}$. Все оставшиеся строки назовем $\\textit{короткими}$.

Иногда в задаче возникают ситуации, когда мы умеем решать ее когда
какое-то свойство \< $\\sqrt{N}$ и больше $\\sqrt{N}$. Данный
подход и называется корневой декомпозицией(оптимизацией).

Самыми простыми и наиболее известными применениями данной оптимизации
являются : алгоритм проверки на простоту чисел(рассмотрим делители \<
$\\sqrt{N}$ и больше, но так как для любого делителя больше корня можно
найти делитель меньше корня =\> нам надо честно рассмотреть только
первые) и например факт, что если суммарная длина строк = $N$, то
различных длин строк будет не более $\\sqrt{N}$ или если вы увидели
ограничение $A B \\le N$, то одно из чисел \< $\\sqrt{N}$.

#### Тяжелые и легкие вершины

Назовем $\\textit{тяжелой}$ вершину, имеющую более $\\sqrt{E}$ соседей.
Все оставшиеся вершины назовем $\\textit{легкими}$. {2} = E$</nowiki>,
чего не может быть. }}

#### Нахождение количества треугольников в графе за $O(E \\sqrt E)$

Мысленно разобьем все вершины графа на легкие и тяжелые. Заметим, что
треугольников, образованных только тяжелыми вершинами, всего
$O(E\\sqrt{E})$, как $C^3_{\\sqrt{E}}$. Теперь рассмотрим треугольники,
которые содержат в себе легкие вершины. В таком треугольнике точно будут
два ребра, инцидентных легкой вершине. Сколько таких пар может быть?
Всего таких ребер $O(E)$, при этом для каждого ребра парными могут
быть только $O(\\sqrt{E})$ ребер, в силу степени легкой вершины. Таким
образом, \\textit{число треугольников в графе равно} $O(E \\sqrt{E})$.
Каким алгоритмом их искать? Можно явно провести процесс, описанный
выше, но это не самое приятное в реализации решение этой задачи.

Можно переориентировать ребра от вершин с меньшей степенью к вершинам с
большей. Теперь верно следующее

Теперь для каждой вершины пометим ее соседей, после чего запустим поиск
путей длины 2 и будем фиксировать треугольник при нахождении пометки.
Для каждого первого ребра пути мы посмотрим на $O(\\sqrt E)$ ребер,
поэтому итоговая сложность алгоритма $O(E \\sqrt E)$

[Категория:Конспект](Категория:Конспект "wikilink")

Теперь обсудим еще одно решение задачи прибавления и суммы на отрезке.
Допустим, что все запросы даны нам заранее и запросов обновления нет.
Для каждого запроса закинем его в блок, где лежит его левая граница:

``` C++
s_dec[l / s].a.push_back({l, r});
```

Затем внутри каждого блока отсортируем запросы по правой границе. Теперь
давайте пройдемся по каждому блоку, поддерживая текущий отрезок, на
который мы знаем ответ. И если текущий отрезок равен отрезку из
запроса запоминать его, как ответ.

``` C++
struct q {
    int l, r, index;
};

struct block {
    vector<q> a;
};

for(int i = 0; i < q; i++) {
    s_dec[l / s].a.push_back({l, r, i});
}

for(int i = 0; i < s; i++) {
    sort(all(s_dec[i].a), comp);
}

for(int i = 0; i < s; i++) {
    int l = i * s, r = i * s;
    int ans = 0;
    for(int j = 0; j < s_dec[i].a.size(); j++) {
        int tl = s_dec[i].a[j].l, tr = s_dec[i].a[j].r;
        while(r > tr) {
            r--;
            ans -= a[r];
        }
        while(r < tr) {
            ans += a[r];
            r++;
        }
        while(l > tl) {
            l--;
            ans += a[l];
        }
        while(l < tl) {
            ans -= a[l];
            l++;
        }
        answ[s_dec[i].a[j].index] = ans;
}
```

Подумаем над асимптотикой данного алгоритма, для каждого запроса левая
граница пройдет не более, чем длину блока, но при этом правая граница
идет только вперед, а следовательно для одного блока пройдет не более,
чем длину массива, то есть суммарно алгоритм работает за $O(M\\sqrt{N}
+ M\\sqrt{N})$, если размер блока - $\\sqrt{N}$.

Алгоритм Мо может помочь нам в ответе на гораздо более сложные вопросы -
$k$-ая статистика на отрезке, медиана отрезка, наиболее встречающийся
элемент на отрезке и так далее.

Также существуют такие модификации алгоритма Мо, как [Мо
онлайн](Мо_онлайн "wikilink"), [3-Д мо](3-Д_мо "wikilink"),
[Мо на деревьях](Мо_на_деревьях "wikilink").  [Категория:Структуры
данных](Категория:Структуры_данных "wikilink")
[Категория:Конспекты](Категория:Конспекты "wikilink")