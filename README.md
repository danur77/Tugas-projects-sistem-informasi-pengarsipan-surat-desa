# Tugas-projects-sistem-informasi-pengarsipan-surat-desa

### Nama           : Danang Nurcahyo ###
### NIM            : 312210004 ###
### Kelas          : TI.22.A.1 ### 

#FROM LOGIN




					<!-- Simple login form -->
					<form action="" method="post">
						<div class="panel panel-body login-form">
							<div class="text-center">
								<div class="icon-object border-slate-300 text-slate-300"><img src="assets/logo.jpg" alt="Logo Surat Menyurat" width="50"></div>
								<h5 class="content-group">pengarsipan surat masuk & keluar<small class="display-block">Silahkan Masuk</small></h5>
								<?php
								echo $this->session->flashdata('msg');
								?>
							</div>

							<div class="form-group has-feedback has-feedback-left">
								<input type="text" class="form-control" name="username" placeholder="Masukkan Nama Pengguna" required>
								<div class="form-control-feedback">
									<i class="icon-user text-muted"></i>
								</div>
							</div>

							<div class="form-group has-feedback has-feedback-left">
								<input type="password" class="form-control" name="password" placeholder="Masukkan Katasandi" required>
								<div class="form-control-feedback">
									<i class="icon-lock2 text-muted"></i>
								</div>
							</div>

							<div class="col-md-12">
								<!-- <div class="col-md-6">
									<div class="form-group">
										<a href="web/daftar" class="btn btn-primary btn-block"><i class="icon-circle-left2 position-left"></i> Daftar</a>
									</div>
								</div> -->

								<div class="col-md-12">
									<div class="form-group">
										<button type="submit" name="btnlogin" class="btn btn-primary btn-block">Masuk <i class="icon-circle-right2 position-right"></i></button>
									</div>
								</div>
							</div>

							<div class="text-center">
								<!-- <a href="web/lupa_password">Lupa Password??</a> -->
							</div>
						</div>
					</form>
					
					<!-- /simple login form -->


     #BERANDA



     <?php
  $cek    = $user->row();
  $id_user = $cek->id_user;
  $nama    = $cek->nama_lengkap;
  $level   = $cek->level;

  $tgl = date('m-Y');
?>

<!-- Main content -->
<div class="content-wrapper">
  <!-- Content area -->
  <div class="content">

    <!-- Dashboard content -->
    <div class="row">
      <!-- Basic datatable -->
      <div class="panel panel-flat bg-info">
        <div class="panel-heading">
          <h3 class="panel-title">
            <center>
              Sistem Informasi Arsip Surat Masuk dan Surat Keluar Desa
            </center>
          </h3>
        </div>
      </div>
      <!-- /basic datatable -->

      <div class="row">
        <div class="col-lg-12">

          <!-- Quick stats boxes -->
          <div class="row">
            <div class="col-lg-6">
              <!-- Current server load -->
              <div class="panel bg-teal-400">
                <div class="panel-body">
                  <div class="heading-elements">
                    <span class="heading-text"><i class="icon-folder-download2"></i></span>
                  </div>
                  <h3 class="no-margin">
                  <?php
                  if ($level == 'user') {
                    echo number_format($this->db->query("SELECT * FROM tbl_sm WHERE id_user='$id_user'")->num_rows(), 0,",",".");
                  }else{
                    echo number_format($this->db->query("SELECT * FROM tbl_sm")->num_rows(), 0,",",".");
                  }?>
                  </h3>
                  Surat Masuk
                </div>

                <a href="users/sm" style="color:#f1f1f1;text-align:center;">
                <div id="server-load" style="border:1px solid #222;padding:10px;background:#333;">
                    Selengkapnya <i class="icon-circle-right2"></i>
                </div>
                </a>
              </div>
              <!-- /current server load -->
            </div>

            <div class="col-lg-6">
              <!-- Current server load -->
              <div class="panel bg-orange-400">
                <div class="panel-body">
                  <div class="heading-elements">
                    <span class="heading-text"><i class="icon-folder-upload2"></i></span>
                  </div>
                  <h3 class="no-margin">
                  <?php
                  if ($level == 'user') {
                    echo number_format($this->db->query("SELECT * FROM tbl_sk WHERE id_user='$id_user'")->num_rows(), 0,",","."); 
                  }else{
                    echo number_format($this->db->query("SELECT * FROM tbl_sk")->num_rows(), 0,",",".");
                  }?></h3>
                  Surat Keluar
                </div>

                <a href="users/sk" style="color:#f1f1f1;text-align:center;">
                <div id="server-load" style="border:1px solid #222;padding:10px;background:#333;">
                    Selengkapnya <i class="icon-circle-right2"></i>
                </div>
                </a>
              </div>
              <!-- /current server load -->
            </div>

          </div>
          <!-- /quick stats boxes -->

          <div class="row">
            <div class="col-lg-12">

              <div class="calendar"></div>
              <div class="box"></div>
              <br>
            </div>

            <br>
          </div>

        </div>


      </div>

    </div>
    <!-- /dashboard content -->


    <script type="text/javascript">
    $(function() {
      function onClickHandler(date, obj) {
        /**
         * @date is an array which be included dates(clicked date at first index)
         * @obj is an object which stored calendar interal data.
         * @obj.calendar is an element reference.
         * @obj.storage.activeDates is all toggled data, If you use toggle type calendar.
               * @obj.storage.events is all events associated to this date
         */

        var $calendar = obj.calendar;
        var $box = $calendar.parent().siblings('.box').show();
        var text = 'Anda memilih tanggal ';

        if(date[0] !== null) {
          text += date[0].format('DD MMMM YYYY');
        }

        if(date[0] !== null && date[1] !== null) {
          text += ' ~ ';
        } else if(date[0] === null && date[1] == null) {
          text += 'tidak ada';
        }

        if(date[1] !== null) {
          text += date[1].format('DD MMMM YYYY');
        }

        $box.text(text);
      }

      $('.calendar').pignoseCalendar({
        lang: 'ind',
        select: onClickHandler,
        theme: 'blue' // light, dark, blue
      });
    });

    </script>

