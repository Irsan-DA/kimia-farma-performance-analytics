CREATE OR REPLACE TABLE `kimia_farma.tabel_analisa` AS
SELECT
  t.transaction_id,
  PARSE_DATE('%m/%d/%Y', t.date) AS date,
  b.branch_id,
  b.branch_name,
  b.kota,
  b.provinsi,
  b.rating AS rating_cabang,
  t.customer_name,
  p.product_id,
  p.product_name,
  t.price AS actual_price,
  t.discount_percentage,
  CASE
    WHEN t.price <= 50000 THEN 0.10
    WHEN t.price <= 100000 THEN 0.15
    WHEN t.price <= 300000 THEN 0.20
    WHEN t.price <= 500000 THEN 0.25
    ELSE 0.30
  END AS persentase_gross_laba,
  t.price * (1 - t.discount_percentage) AS nett_sales,
  (t.price * (1 - t.discount_percentage)) *
    CASE
      WHEN t.price <= 50000 THEN 0.10
      WHEN t.price <= 100000 THEN 0.15
      WHEN t.price <= 300000 THEN 0.20
      WHEN t.price <= 500000 THEN 0.25
      ELSE 0.30
    END AS nett_profit,
  t.rating AS rating_transaksi
FROM `kimia_farma.kf_final_transaction` t
INNER JOIN `kimia_farma.kf_kantor_cabang` b
  ON t.branch_id = b.branch_id
INNER JOIN `kimia_farma.kf_product` p
  ON t.product_id = p.product_id;
