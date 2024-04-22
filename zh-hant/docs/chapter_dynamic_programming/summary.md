# 小結

- 動態規劃對問題進行分解，並透過儲存子問題的解來規避重複計算，提高計算效率。
- 不考慮時間的前提下，所有動態規劃問題都可以用回溯（暴力搜尋）進行求解，但遞迴樹中存在大量的重疊子問題，效率極低。透過引入記憶化串列，可以儲存所有計算過的子問題的解，從而保證重疊子問題只被計算一次。
- 記憶化搜尋是一種從頂至底的遞迴式解法，而與之對應的動態規劃是一種從底至頂的遞推式解法，其如同“填寫表格”一樣。由於當前狀態僅依賴某些區域性狀態，因此我們可以消除 $dp$ 表的一個維度，從而降低空間複雜度。
- 子問題分解是一種通用的演算法思路，在分治、動態規劃、回溯中具有不同的性質。
- 動態規劃問題有三大特性：重疊子問題、最優子結構、無後效性。
- 如果原問題的最優解可以從子問題的最優解構建得來，則它就具有最優子結構。
- 無後效性指對於一個狀態，其未來發展只與該狀態有關，而與過去經歷的所有狀態無關。許多組合最佳化問題不具有無後效性，無法使用動態規劃快速求解。

**背包問題**

- 背包問題是最典型的動態規劃問題之一，具有 0-1 背包、完全背包、多重背包等變種。
- 0-1 背包的狀態定義為前 $i$ 個物品在容量為 $c$ 的背包中的最大價值。根據不放入背包和放入背包兩種決策，可得到最優子結構，並構建出狀態轉移方程。在空間最佳化中，由於每個狀態依賴正上方和左上方的狀態，因此需要倒序走訪串列，避免左上方狀態被覆蓋。
- 完全背包問題的每種物品的選取數量無限制，因此選擇放入物品的狀態轉移與 0-1 背包問題不同。由於狀態依賴正上方和正左方的狀態，因此在空間最佳化中應當正序走訪。
- 零錢兌換問題是完全背包問題的一個變種。它從求“最大”價值變為求“最小”硬幣數量，因此狀態轉移方程中的 $\max()$ 應改為 $\min()$ 。從追求“不超過”背包容量到追求“恰好”湊出目標金額，因此使用 $amt + 1$ 來表示“無法湊出目標金額”的無效解。
- 零錢兌換問題 II 從求“最少硬幣數量”改為求“硬幣組合數量”，狀態轉移方程相應地從 $\min()$ 改為求和運算子。

**編輯距離問題**

- 編輯距離（Levenshtein 距離）用於衡量兩個字串之間的相似度，其定義為從一個字串到另一個字串的最少編輯步數，編輯操作包括新增、刪除、替換。
- 編輯距離問題的狀態定義為將 $s$ 的前 $i$ 個字元更改為 $t$ 的前 $j$ 個字元所需的最少編輯步數。當 $s[i] \ne t[j]$ 時，具有三種決策：新增、刪除、替換，它們都有相應的剩餘子問題。據此便可以找出最優子結構與構建狀態轉移方程。而當 $s[i] = t[j]$ 時，無須編輯當前字元。
- 在編輯距離中，狀態依賴其正上方、正左方、左上方的狀態，因此空間最佳化後正序或倒序走訪都無法正確地進行狀態轉移。為此，我們利用一個變數暫存左上方狀態，從而轉化到與完全背包問題等價的情況，可以在空間最佳化後進行正序走訪。