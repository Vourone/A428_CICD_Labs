node { // Memulai pipeline Jenkins baru
  docker.image('node:16-buster-slim').inside('-p 3000:3000') { // Menggunakan image Docker node:16-buster-slim dan memetakan port 3000
    stage('Build') { // Mendefinisikan tahap Build
      sh 'npm install' // Menjalankan perintah npm install untuk menginstal dependencies
    }
    stage('Test') { // Mendefinisikan tahap Test
      sh './jenkins/scripts/test.sh' // Menjalankan skrip test
    }
    stage('Manual Approval') { // Mendefinisikan tahap Manual Approval
      input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed' // Menunggu persetujuan manual untuk melanjutkan ke tahap Deploy
    }
    stage('Deploy') { // Mendefinisikan tahap Deploy
      sh './jenkins/scripts/deliver.sh' // Menjalankan skrip deploy
      sleep 60 // Menunggu selama 60 detik
      sh './jenkins/scripts/kill.sh' // Menjalankan skrip kill untuk menghentikan layanan yang sedang berjalan
    }
  }
}
