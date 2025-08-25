# Java Yüksek CPU Kullanımı Teşhis Adımları (Diagnostic Cheatsheet)

Bu belge, bir Java uygulamasının neden %100 CPU kullandığını tespit etmek için kullanılan komutları ve adımları örneklerle açıklar.

---

## 🔍 1. Java PID'sini Bulma

### `jps -l`
Java process'lerini listeler.
```bash
jps -l
```
**Örnek çıktı:**
```
8 com.example.MyApp
```

### `ps aux | grep java`
Alternatif olarak süreç ID'sini öğrenmek için:
```bash
ps aux | grep java
```

---

## 🧵 2. Thread Dump Alma

### `jstack <pid>`
Java uygulamasının thread dump’ını al:
```bash
jstack 8 > dump.txt
```

---

## 🔎 5. Problemli Thread'i Bulma

### dump.txt içinde `nid=0x21c` ara
```text
"XNIO-2 task-1" #78 daemon prio=3 os_prio=0 cpu=711889.23ms elapsed=72304.20s tid=... nid=0x21c runnable
   java.lang.Thread.State: RUNNABLE
   at java.util.regex.Matcher.replaceAll
   at ...
```

---

---

## ✅ Özet

| Adım | Açıklama |
|------|----------|
| jps / ps | Java PID'yi bul |
| jstack | Dump al |
| nid=0x... | Problemli thread’i analiz et |
| Kod İncelemesi | Sonsuz döngü, put/merge hataları kontrol et |

---

Bu rehberle yüksek CPU sorunlarını hızlıca izole edip çözümleyebilirsin.
