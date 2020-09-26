# SQL クエリ 備忘録

参照：
[Progate](https://prog-8.com)
環境：
macOS(Catalina)

---
## 1. 基本

#### 【クエリ基本形】
```SQL
SELECT カラム名

FROM テーブル名

WHERE 条件

ORDER BY 並べたいカラム名, 並べ方(ASC or DESC)

LIMIT データの件数
;
```

#### 【データ条件】
```SQL
-- ★LIKE演算子
-- ワイルドカード(%)で前方一致、後方一致ができる
WHERE name LIKE 文字列
-- (例) hogeを含む
WHERE name LIKE "%hoge%"

-- ★NOT演算子
WHERE NOT 条件

-- ★IS NULL / IS NOT NULL
WHERE name IS NULL
WHERE name IS NOT NULL

-- ★AND / OR 演算子
WHERE 条件 AND 条件
WHERE 条件 OR 条件
```

---

## 2. データの加工・分析

#### 【DISTINCT】
- 重複するデータを除く
```SQL
SELECT DISTINCT(name)
FROM purchases;
```

#### 【SUM関数】
- 合計する
```SQL
SELECT SUM(price)
FROM purchases;
```

#### 【AVG関数】
- 平均する
```SQL
SELECT AVG(price)
FROM purchases;
```

#### 【COUNT関数】
- 集計する
```SQL
SELECT COUNT(price)
FROM purchases;
```

#### 【MAX・MIN関数】
- 最大値・最小値を取得する
```SQL
SELECT MAX(price)
FROM purchases;

---

SELECT MIN(price)
FROM purchases;
```

#### 【GROUP BY】
- データをグループ化
```SQL
SELECT SUM(price), purchased_at
FROM purchases
GROUP BY purchased_at;
```

#### 【HAVING】
- グループ化したデータを絞り込む
```SQL
SELECT SUM(name)
FROM purchases;
GROUP BY purchased_at
HAVING SUM(price) > 2000;
```