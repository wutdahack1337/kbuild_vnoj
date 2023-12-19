# kbuild_vnoj
Kbuild problem và những gì t học được

T đang trong quá trình học [LCA](cp-algorithms.com/graph/lca.html), t nghĩ được ý tưởng để tìm LCA là đi lên từng bước một O(q * n).
  
Tiếp theo t tìm cách tối ưu thuật, t tự hỏi thay vì đi lên từng bước, tại sao lại không đi lên nhiều bước cùng một lúc. Câu hỏi cần phải trả lời lúc này là: đi lên bao nhiêu bước cùng lúc là hợp lý? T nghĩ tới [chia căn](vnoi.info/wiki/algo/data-structures/sqrt-decomposition.md) - đại khái là chia một đoạn to thành sqrt đoạn nhỏ rồi mình thao tác trên sqrt đoạn nhỏ đó. T áp dụng [ý tưởng](vnoi.info/wiki/translate/topcoder/Range-Minimum-Query-and-Lowest-Common-Ancestor.md#thuật-toán-o-n-o-sqrt-n-1) đó vào LCA cho ra O(q * sqrt(n)).
  
T đã nghĩ như thế là đã đủ tốt, có thể giải quyết được tất cả bài toán rồi. Nhưng mọi chuyện không đơn giản như vậy khi t gặp bài [Kbuild](oj.vnoi.info/problem/kbuild), với time limit là 0.6s và số đỉnh là 2 * 10^5, thuật toán LCA chia căn của t đã bị đánh bại, và cộng thêm ý tưởng đánh dấu cạnh đã đi của t quá ngu, t cần tìm một lối đi mới. T nhận ra mình có 2 vấn đề cần giải quyết:
1. Tối ưu LCA
2. Thay đổi thuật đánh dấu cạnh đã đi

Đầu tiên là tối ưu LCA, t lên vnoi tìm đọc một hướng đi khác để tìm LCA, t tìm thấy một thứ hay ho gọi là [Binary Jumping/Lifting](vnoi.info/wiki/algo/data-structures/lca-binlift.md#binary-lifting-nâng-nhị-phân) - t nhận ra nó như là một phiên bản nâng cấp của chia căn. Thay vì bước đi một lúc sqrt bước như chia căn, Binary Jumping sẽ bước đi một lúc là 2^k bước (đủ lớn để tối ưu và đủ bé để bước chính xác). "Ơ rê ka", đây chính là thứ t cần tìm, ý tưởng này có thể thay thế hoàn toàn chia căn với tốc độ nhanh hơn rất nhiều, độ phức tạp của thuật toán đã giảm từ O(q * sqrt(n)) xuống còn O(q * log2(n)). Quá đã ~~  
  
Thứ hai là thay đổi thuật đánh dấu cạnh đã đi của t, vì t đã bí ý tưởng nên đành mò vào code mẫu của vnoj, t chọn xem code a RR, đọc code xong, ngẫm nghĩ một hồi, t mới thấy hay vl. Đây là cách a ấy làm, tương tự như một bài toán được xử lý trên đoạn thẳng, đó là bài toán cho n cuộc họp thời gian là a_i tới b_i, hỏi tại thời điểm c_i có bao nhiêu cuộc họp đang diễn ra, cách giải bài này là ++f[a_i], --f[b_i+1], rồi sau đó prefix sums là ra được ans, **mấu chốt** ở đây là chỉ cần đánh dấu 2 đầu a_i và b_i sau đó prefix sums đã có thể đánh dấu được thời gian a_i -> b_i. Lấy **mấu chốt** đó làm ý tưởng chính, nhưng mà lúc này là một cái cây, vậy là bây giờ là ý tưởng là đánh dấu ++f[s], ++f[t], f[LCA(s, t)] -= 2 sau đó ta prefix sums trên cây, những cạnh nào đã được đi qua sẽ > 0, còn chưa được đi qua sẽ = 0. Quá hay ^.^  

Tóm lại, qua bài Kbuild t đã học được:
- Cách nâng cấp thuật toán LCA chia căn
- Cách đánh dấu những cạnh đã đi rồi trên cây một cách thông minh

Thế thôi ~~
