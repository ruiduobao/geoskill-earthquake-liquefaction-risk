# 地震液化风险评估 | Earthquake Liquefaction Risk

用 Youd 简化法评估砂土液化：循环应力比 CSR = 0.65·(PGA/g)·rd(z)·gw（rd 应力折减、gw 浅地下水放大），循环阻抗比 CRR 随 SPT 击数 N 增大（越密实越抗液化），安全系数 FS=CRR/CSR（<1 判定液化），再按 Iwasaki 深度权重积分得液化指数 LPI（≥0）。PGA 越高 → FS 越低 → LPI 越高（正相关）。

## 依赖

```bash
pip install numpy rasterio scipy
```

## 使用方法

### 基本用法（合成数据，离线）

```bash
python geoskill-earthquake-liquefaction-risk.py --bbox 116.0 39.0 117.0 40.0 --synthetic --output-dir ./out
```

### 更多示例

```bash
python geoskill-earthquake-liquefaction-risk.py --bbox 116 39 117 40 --synthetic --output-dir ./out
python geoskill-earthquake-liquefaction-risk.py --input site.tif --depth 5 --output-dir ./out
python geoskill-earthquake-liquefaction-risk.py --bbox 116 39 117 40 --depth 3 --fines 20 --synthetic --output-dir ./out
python geoskill-earthquake-liquefaction-risk.py --bbox 117 39 118 40 --synthetic --quiet --output-dir ./out
```

## 输出

| 文件 | 格式 | 说明 |
|---|---|---|
| `liquefaction_index.tif` | GeoTIFF | 液化指数 LPI（≥0） |
| `factor_of_safety.tif` | GeoTIFF | 安全系数 FS（<1 液化） |
| `liquefaction_params.json` | JSON | 评估深度/细粒含量/平均地下水位 |

每次运行还会产出 `output-manifest.json`（运行清单，含输入/产物/QA 摘要）。

## 数据源 / Source

真实模式读取多波段 GeoTIFF（band1=PGA(g)、band2=SPT N值、band3=地下水位埋深m）；合成模式离线生成场地。

## 隐私声明 / Privacy

- 默认离线运行，`--synthetic` 模式完全无网络。
- 所有处理在本地完成，不上传任何用户数据。

## License

MIT
