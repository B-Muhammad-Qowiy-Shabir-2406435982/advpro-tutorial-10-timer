## Experiment 1.2: Memahami Cara Kerja Executor

Setelah menambahkan:

println!("Qowiy's Komputer: hey hey");

tepat setelah spawner.spawn(...), teks hey hey muncul lebih dahulu sebelum done!.

Hal ini terjadi karena spawner.spawn(...) hanya memasukkan async task ke dalam queue executor, bukan langsung menjalankannya sampai selesai. Program utama tetap melanjutkan eksekusi dan mencetak hey hey.

Setelah itu, executor menjalankan async task. Task tersebut mencetak howdy!, menunggu selama dua detik menggunakan TimerFuture, lalu mencetak done!.

## Experiment 1.3: Multiple Spawn dan Fungsi drop(spawner)

`Spawner` digunakan untuk memasukkan task async ke dalam queue executor, sedangkan `executor` bertugas mengambil dan menjalankan task tersebut.

Ketika beberapa task di-spawn sekaligus, executor akan menjalankan semuanya secara asynchronous. Pesan `howdy` muncul lebih dahulu karena dicetak sebelum timer selesai. Setelah sekitar dua detik, pesan `done` muncul karena `TimerFuture` telah selesai dijalankan.

Perintah:

drop(spawner);

sangat penting karena memberi tahu executor bahwa tidak ada task baru yang akan ditambahkan lagi. Jika drop(spawner) dihapus, executor dapat terus menunggu task baru sehingga program tidak berhenti dengan benar.