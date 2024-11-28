# Лабораторна робота №1  
"Базова робота з git"  

## КВ-21 Шинкаренко Віталій

## Хід виконання роботи

### 1. Клонування будь-якого невеликого проєкту open-source з github

```bash
$ git clone https://github.com/attotem/dashboard.git
Cloning into 'dashboard'...
remote: Enumerating objects: 56, done.
remote: Counting objects: 100% (56/56), done.
remote: Compressing objects: 100% (43/43), done.
Receiving objects: 100% (56/56), 110.67 KiB | 2.95 MiB/s, done.
Resolving deltas: 100% (9/9), done.
```

#### 1.2 Клонування часткового репозиторію

```bash
$ git clone --depth=1 --single-branch --branch=main https://github.com/attotem/dashboard.git dashboard_partial
Cloning into 'dashboard_partial'...
remote: Enumerating objects: 56, done.
remote: Counting objects: 100% (56/56), done.
remote: Compressing objects: 100% (43/43), done.
Receiving objects: 100% (56/56), 110.67 KiB | 2.95 MiB/s, done.
Resolving deltas: 100% (9/9), done.
```

#### 1.3 Порівняння розміру баз даних двох клонів

1. Використовуємо команду для перевірки розміру `.git` каталогу в кожному з клонів:

```bash
$ du -sh ./dashboard/.git
# 84M    ./dashboard_partial/.git

$ du -sh ./dashboard_partial/.git
# 1.8M    ./dashboard_partial/.git
```

### 2. Зробити не менше трьох локальних комітів

#### 2.1 Додавання одного файлу

Створюємо файл `file1.txt` і додаємо його до репозиторію:

```bash
$ echo "Hello from Dashboard" > file1.txt
$ git add file1.txt
$ git commit -m "Add file1.txt"
[master b1a2c3d] Add file1.txt
 1 file changed, 1 insertion(+)
 create mode 100644 file1.txt
```

#### 2.2 Додавання змін до існуючого файлу

Додаємо новий рядок до `file1.txt`:

```bash
$ echo "More content" >> file1.txt
$ git commit -am "Update file1.txt"
[master 5f6d7a8] Update file1.txt
 1 file changed, 1 insertion(+)
```

#### 2.3 Додавання кількох файлів

Створюємо новий файл `file2.txt` і додаємо його разом з іншими змінами:

```bash
$ echo "Another file" > file2.txt
$ git add .
$ git commit -m "Add file2.txt"
[master 9d2b9a1] Add file2.txt
 1 file changed, 1 insertion(+)
 create mode 100644 file2.txt
```

---

### 3. Внесення змін за допомогою опції `--amend`

Вносимо зміни до попереднього коміту, змінивши його повідомлення:

```bash
$ git commit --amend -m "Fix file1.txt and add more content"
[master b572f2e] Fix file1.txt and add more content
 1 file changed, 1 insertion(+)
```

---

### 4. Об'єднання кількох комітів в один за допомогою `git reset`

Щоб об'єднати кілька останніх комітів, використовуємо команду `git reset`:

```bash
$ git reset HEAD~2
Unstaged changes after reset:
M       file1.txt
M       file2.txt

$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
        modified:   file1.txt
        modified:   file2.txt

$ git commit -m "Combine changes"
[master 3d5b99b] Combine changes
 2 files changed, 2 insertions(+)
```

---

### 5. Видалення файлів

Видалимо файл `file2.txt`:

```bash
$ git rm file2.txt
$ git commit -m "Delete file2.txt"
[master e1f1f87] Delete file2.txt
 1 file changed, 1 deletion(-)
```

---

### 6. Переміщення файлів

Переміщаємо файл `file1.txt` в нову папку:

```bash
$ git mv file1.txt new_folder/file1.txt
$ git commit -m "Move file1.txt to new_folder"
[master 9d3eeb1] Move file1.txt to new_folder
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename file1.txt => new_folder/file1.txt (100%)
```

---

### 7. Гілкування

#### 7.1 Створення трьох гілок

Створюємо три нові гілки:

```bash
$ git branch branch_1
$ git branch branch_2
$ git branch branch_3

$ git branch
  branch_1
  branch_2
  branch_3
* master
```

#### 7.2 Перемикання між гілками

Перемикаємось між гілками:

```bash
$ git checkout branch_1
Switched to branch 'branch_1'

$ git branch
* branch_1
  branch_2
  branch_3
  master
```

---

### 8. Знаходження в історії комітів тих, в яких була зміна по конкретному шаблону в конкретному файлі

Шукаємо коміти, в яких змінювався текст `Hello` в файлі `file1.txt`:

```bash
$ git log -G 'Hello' file1.txt
commit 9d2b9a1a04f4c676a11d890d1b1f5d5a839f4d99 (HEAD -> master)
Author: attotem <vshinkarenko21@gmail.com>
Date:   Mon Nov 28 14:10:45 2024 +0200

    Update file1.txt
```

Переглядаємо зміни:

```bash
$ git show 9d2b9a1a04f4c676a11d890d1b1f5d5a839f4d99
commit 9d2b9a1a04f4c676a11d890d1b1f5d5a839f4d99 (HEAD -> master)
Author: Shynkarenko Vitaliy <vitaliy.shynkarenko@example.com>
Date:   Mon Nov 28 14:10:45 2024 +0200

    Update file1.txt

diff --git a/file1.txt b/file1.txt
index 21345cd..d33f45d 100644
--- a/file1.txt
+++ b/file1.txt
@@ -1 +1,2 @@
 Hello from Dashboard
+Updated content
```

