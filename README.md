## Experiment 1.2: Memahami Cara Kerja Executor

Setelah menambahkan:

println!("Qowiy's Komputer: hey hey");

tepat setelah spawner.spawn(...), teks hey hey muncul lebih dahulu sebelum done!.

Hal ini terjadi karena spawner.spawn(...) hanya memasukkan async task ke dalam queue executor, bukan langsung menjalankannya sampai selesai. Program utama tetap melanjutkan eksekusi dan mencetak hey hey.

Setelah itu, executor menjalankan async task. Task tersebut mencetak howdy!, menunggu selama dua detik menggunakan TimerFuture, lalu mencetak done!.