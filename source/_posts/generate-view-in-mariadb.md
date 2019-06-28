---
title: generate view in mariadb
date: 2018-11-07 08:50:17
tags:
---

{% codeblock %}
CREATE ALGORITHM=UNDEFINED DEFINER=`root`@`localhost` SQL
SECURITY DEFINER VIEW `example` AS (select `t`.`id` AS `id`,`t`.`s` AS `s` from
`t`)
{% endcodeblock %}


{% codeblock %}
CREATE ALGORITHM=UNDEFINED SQL SECURITY DEFINER VIEW summary_pesanan AS (SELECT pesanan.id, pesanan.tanggal, pesanan.pengguna_id, pesanan.produk_id, pesanan.jumlah, Format(pesanan.total_bayar, '##.##0') AS total_bayar, pesanan.keterangan, produk.nama, produk.foto FROM pesanan INNER JOIN produk ON pesanan.produk_id = produk.id WHERE pesanan.`status` = 0 AND substr(tanggal,1,10)=substr(current_timestamp(),1,10) ORDER BY pesanan.tanggal DESC)
{% endcodeblock %}



CREATE ALGORITHM=UNDEFINED SQL SECURITY DEFINER VIEW summary_tempat_usaha AS (
SELECT epasar_lease_requests.id_tenant, epasar_lease_requests.id_unit, epasar_lease_requests.request_number, epasar_units.id_pasar FROM epasar_lease_requests
JOIN epasar_units
ON epasar_lease_requests.id_unit = epasar_units.id
WHERE epasar_lease_requests.status = 4 AND epasar_lease_requests.approval_level = 3 

)



