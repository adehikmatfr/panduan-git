# Panduan Penggunaan Git

basic perintah git, setelah mengerti perintah dasar ini kamu bisa lanjut belajar. 
1. bagaimana cara memperbaiki conflict
2. graph di git
3. stash 

* [Mengunduh repository ke dalam komputer](http://https://github.com/adehikmatfr/panduan-git#mengunduh-repository)
* [Memperbarui repository yang telah diunduh](https://github.com/adehikmatfr/panduan-git#memperbarui-repository)
* [Mengunggah perubahan ke dalam repository](https://github.com/adehikmatfr/panduan-git#mengunggah-perubahan)
* [Menghapus file](https://github.com/adehikmatfr/panduan-git#menghapus-file)
* [Branching](https://github.com/adehikmatfr/panduan-git#branching)
* [Perintah tambahan](https://github.com/adehikmatfr/panduan-git#perintah-tambahan)
* [gitignore](https://github.com/adehikmatfr/panduan-git#gitignore)

## Mengunduh Repository

Unduh repository ke dalam komputer menggunakan perintah `git clone`. Url
repository dapat dilihat di dalam repository yang diinginkan.
secara default folder tujuan yang akan terbuat adalah last path dari url git. 

```
git clone <url repository> <folder tujuan>
```

#### Contoh

```
user@host:~$ git clone https://github.com/adehikmatfr/panduan-git.git git-guid
Cloning into 'git-guid'...
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 4 (delta 0), reused 4 (delta 0), pack-reused 0
Unpacking objects: 100% (4/4), done.
```

## Memperbarui Repository

Perbarui repository yang telah diunduh ke dalam komputer menggunakan perintah
`git pull`.

```
git pull origin <nama branch>
```

#### Contoh

```
git pull https://github.com/adehikmatfr/panduan-git.git master
From https://github.com/adehikmatfr/panduan-git/instagram
 * branch            master     -> FETCH_HEAD
Already up-to-date.
```

## Mengunggah Perubahan

Jangan lupa untuk melakukan pull terlebih dahulu sebelum melakukan push.
untuk menambahkan semua perubahan `<nama file>` bisa di ubah dengan .

**Tambah file baru atau ubah file**

```
git add <nama file>
```

**Konfirmasi penambahan atau perubahan file**

```
git commit -m "<pesan commit>"
```

**Kirim perubahan ke dalam repository**

```
git push origin <nama branch>
```

#### Contoh

```
user@host:~$ git add README.md

user@host:~$ git commit -m "Mengedit readme"
[master 224c510] Mengedit readme
 1 file changed, 1 insertion(+)
 update mode 100644 README.md

user@host~$ git push origin master
Counting objects: 3, done.
Delta compression using up to 16 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 271 bytes | 0 bytes/s, done.
Total 2 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local objects.
To https://github.com/adehikmatfr/panduan-git.git
   fec3a1f..224c510  master -> master
```

## Menghapus File

Hapus file dari repository menggunakan perintah `git rm`, diikuti dengan `git commit`, dan `git push`.

```
git rm <nama file>
```

#### Contoh

```
user@host~$ git rm README.md
rm 'README.md'

user@host~$ git commit -m
[master 658a76e] Menghapus README
 1 file changed, 1 deletion(-)
 delete mode 100644 README.md

user@host~$
Counting objects: 3, done.
Delta compression using up to 16 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 236 bytes | 0 bytes/s, done.
Total 2 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local objects.
To https://github.com/adehikmatfr/panduan-git.git
   224c510..658a76e  master -> master
```

## Branching

Branch digunakan untuk mengembangkan fitur baru atau mengubah source code tanpa
memberikan dampak kepada branch lain. Branch master adalah branch default dari
sebuah repository. Gunakan branch lain untuk melakukan pengembangan dan
gabungkan kembali ke dalam branch master.

### Melihat branch yang terdapat di dalam repository lokal

```
git branch
```

```
user@host~$ git branch
* master
```

Tanda asterisk (\*) menandakan branch yang sedang aktif.

### Melihat branch yang terdapat di dalam repository lokal

```
git branch -r
```

```
user@host~$ git branch -r
  origin/HEAD -> origin/master
  origin/master
```

### Membuat branch baru di dalam repository lokal dan kirim ke repository remote

**Buat branch baru**

```
git branch <nama branch baru>
```

**Aktifkan branch baru**

```
git checkout <nama branch baru>
```

**Konfirmasi perubahan**

```
git commit -m "<pesan konfirmasi>"
```

**Unggah branch baru ke dalam repository remote**

```
git push origin <nama branch baru>
```

#### Contoh

```
user@host~$ git branch development

user@host~$ git checkout development
Switched to branch 'development'

user@host~$ git commit -m "Menambah branch development"
On branch development
nothing to commit, working tree clean

user@host~$ git push origin development
Total 0 (delta 0), reused 0 (delta 0)
remote:
remote: Create pull request for new:
remote:   https://github.com/adehikmatfr/panduan-git/pull-requests/new?source=new&t=1
remote:
To https://github.com/adehikmatfr/panduan-git.git
 * [new branch]      development -> development
```

### Menambahkan branch dari repository remote ke dalam repository lokal

```
git branch <nama branch remote>
git pull origin <nama branch remote>
git checkout <nama branch remote>
```

#### Contoh

```
user@host~$ git branch development

user@host~$ git pull origin development
 * branch            new        -> FETCH_HEAD
 * [new branch]      new        -> origin/development
Already up-to-date.

user@host~$ git checkout development
Switched to branch 'development'
```

### Menggabungkan branch lain ke dalam branch aktif

**Aktifkan branch yang diinginkan**

```
git checkout <nama branch aktif>
```

**Perbarui branch local**

```
git pull origin <nama branch aktif>
```

**Penggabungan**

```
git merge <nama branch yang akan digabungkan>
```

**Cek dan selesaikan konflik akibat penggabungan branch**

```
git status
```

**Konfirmasi dan unggah penggabungan branch**

```
git commit -m "<pesan konfirmasi>" -a
git push origin <nama branch aktif>
```

#### Menghapus branch

**Pada repository remote**

```
git push origin :<nama branch>
```

**Pada repository lokal**

```
git branch <nama branch> -d
```

## Perintah tambahan

Dapatkan status dari repository

```
git status
```

Dapatkan log dari sebuah repository

```
git log
```

## gitignore
Ada kalanya kita melihat file gitignore di suatu repository. Apakah itu gitignore? gitignore adalah file yang berisi instruksi kepada git repository untuk tidak men-track files tertentu. Ini sangat berguna untuk meng-exclude files yang mungkin tidak berguna atau tidak perlu di push ke repository. Contoh: .DS_Store di Mac, binary files, `__pycache__`, etc. 

File gitignore dimulai dengan titik (`.`) di Unix-based system (Mac dan Linux) untuk menandakan dia adalah hidden file. Di Windows, buat file gitignore dengan memberi nama `.gitignore.`.

#### Contoh

Untrack file tertentu
```
# tagar digunakan untuk commenting
# Mac
.DS_Store

# Spreadsheet
*.xls
*.xlsx

# Compressed file
*.zip
*.rar
*.gz
```

Untrack folder tertentu
```
# tagar digunakan untuk commenting
# python
__pycache__/

# virtual environment
env/
venv/
```

Contoh koleksi gitignore yang berguna  
https://github.com/github/gitignore



<!-- EDIT HERE TO TRY -->

<!-- EDIT HERE TO TRY -->