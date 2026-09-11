# K4 — Ngày 1: Bài Tập & Phản Ánh
## Khám Phá LLM API | Phiếu Thực Hành

**Thời lượng:** 4 tiếng
**Cách làm:** Trả lời từng câu ngay sau khi hoàn thành block tương ứng —
đừng để dồn hết về cuối buổi. Thay dòng `*Câu trả lời của bạn*` bằng câu
trả lời thật (chấm tự động sẽ đếm số câu đã trả lời).

---

## Block 1 — API Cơ Bản (trả lời sau Checkpoint 1)

### Câu 1.1 — Độ nhạy của temperature
Gọi `call_openai` với temperature 0.0, 0.5, 1.0 và 1.5 dùng prompt
**"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**
>0.0: Việt Nam có hệ thống hang động ngầm dài 2.5 km dưới thành phố Hội An, được gọi là “đường hầm Củ Chi của miền Trung” và được sử dụng để vận chuyển thực phẩm và người trong thời kỳ chiến tranh. Đây là một trong những mạng lưới đường hầm ngầm dài nhất và phức tạp nhất ngoài Củ Chi.
0.5: Việt Nam là nơi sinh ra “phở” – món ăn quốc hồn quốc túy, nhưng thực tế, phở còn được cho là có nguồn gốc từ món “bánh tráng xào” của người Hoa thời kỳ thực dân Pháp, và đã dần phát triển thành món ăn độc đáo chỉ có ở Việt Nam. 🌿🍜
1.0:Việt Nam là quốc gia sản xuất cà phê lớn thứ hai trên thế giới, chỉ sau Brazil, và cà phê robusta của miền Nam được ưa chuộng nhờ hương vị mạnh mẽ và đậm đà.
1.5:Việt Nam là quốc gia duy nhất trên thế giới có **hai mùa mưa** trong cùng một năm: mùa mưa miền Bắc (từ tháng 5‑6 đến tháng 8‑9) và mùa mưa miền Nam (từ tháng 5‑6 đến tháng 10‑11), tạo nên sự đa dạng sinh thái và cảnh quan phong phú. 🌧️🌿


**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> Khi tăng temperature từ 0.0 lên 1.5, câu trả lời dần trở nên đa dạng, sáng tạo hơn và có nhiều chi tiết, nhưng đồng thời cũng giảm độ chính xác và có khả năng lạc đề; ở temperature thấp (0.0) mô hình cho ra câu ngắn gọn, chính xác và ít sai, trong khi ở mức trung bình (0.5-1.0) câu trả lời cân bằng giữa tính chính xác và sự phong phú.



### Câu 1.2 — Chọn temperature cho sản phẩm
**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
>Đối với chatbot hỗ trợ khách hàng, mình thường đặt **temperature khoảng 0.2‑0.3**.  

- **Giữ tính nhất quán:** nhiệt độ thấp giúp câu trả lời ổn định, tránh đưa ra những phản hồi lạ hoặc không liên quan.  
- **Đảm bảo độ chính xác:** khách hàng cần thông tin rõ ràng, đúng mục đích, nên giảm thiểu sự "sáng tạo" không cần thiết.  
- **Nhanh chóng và an toàn:** giảm khả năng sinh ra nội dung nhạy cảm hoặc sai sót.

Như vậy, mức temperature thấp sẽ mang lại trải nghiệm hỗ trợ khách hàng chuyên nghiệp và tin cậy.




### Câu 1.3 — Đánh đổi chi phí
Kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người gọi API 3 lần,
mỗi lần trung bình ~350 token đầu ra.

**Ước tính GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này? Nêu một
trường hợp GPT-4o xứng đáng với chi phí và một trường hợp nên dùng mini:**
>GPT‑4o tốn khoảng **5 lần** chi phí so với GPT‑4o‑mini cho cùng một khối lượng công việc.
>**Khi nào nên chọn GPT‑4o (đáng trả tiền hơn):**  
>- **Yêu cầu độ phức tạp cao** – ví dụ soạn thảo báo cáo nghiên cứu, lập trình phức tạp, phân tích dữ liệu đa chiều, hay tạo nội dung sáng tạo đòi hỏi “độ sâu” và “độ chính xác” tối đa.  
>- **Cần kiến thức cập nhật** – các câu hỏi liên quan tới xu hướng công nghệ mới, luật pháp, y tế gần đây mà mô hình siêu lớn thường có độ phủ tốt hơn.  
>- **Ứng dụng khách hàng cuối** – chatbot hỗ trợ khách hàng doanh nghiệp, nơi mỗi phản hồi cần độ tin cậy, ngữ cảnh liên tục và khả năng xử lý lỗi tốt; chi phí cao hơn được bù đắp bởi trải nghiệm người dùng tốt hơn và giảm thiểu sai sót.

>**Khi nào nên dùng GPT‑4o‑mini (tiết kiệm chi phí):**  
>- **Nhiệm vụ đơn giản, lặp lại** – ví dụ trả lời câu hỏi FAQ, tóm tắt ngắn gọn, tạo tiêu đề, dịch thuật cơ bản, hoặc gợi ý từ khóa.  
>- **Khối lượng lớn, ngân sách hạn chế** – khi xử lý hàng triệu yêu cầu mỗi ngày (ví dụ phân loại bình luận, gán nhãn dữ liệu), chi phí mỗi token của mini giúp giảm đáng kể tổng chi phí.  
>- **Phát triển prototype hoặc thử nghiệm** – dùng mini để nhanh chóng kiểm thử ý tưởng, sau đó nếu cần chất lượng cao hơn mới chuyển sang GPT‑4o.  

---

## Block 2 — System Prompt & Token (trả lời sau Checkpoint 2)

### Câu 2.1 — Sức mạnh của persona
Gọi `chat_with_system_prompt` hai lần với cùng câu hỏi
**"Giải thích blockchain là gì?"** nhưng hai system prompt khác nhau:
- "Bạn là giáo viên tiểu học, giải thích thật đơn giản cho trẻ 8 tuổi."
- "Bạn là chuyên gia tài chính, trả lời chuyên sâu bằng thuật ngữ kỹ thuật."

**Hai phản hồi khác nhau như thế nào (độ dài, từ vựng, ví dụ)? System prompt
ảnh hưởng đến hành vi model ra sao?** (3–4 câu)
> Blockchain là một chuỗi các khối dữ liệu liên kết với nhau theo thứ tự thời gian, mỗi khối chứa:

1. **Giao dịch** (hoặc dữ liệu) đã được xác nhận.  
2. **Mã băm** (hash) của khối hiện tại, tạo ra một dấu vân tay duy nhất.  
3. **Mã băm của khối trước**, giúp các khối “nối” thành chuỗi.

Khi một khối mới được tạo, nó phải được **được mạng lưới (nhiều nút) xác thực** thông qua các thuật toán đồng thuận (ví dụ Proof‑of‑Work). Khi đã đồng ý, khối được gắn vào chuỗi và không thể sửa đổi mà không thay đổi toàn bộ các khối sau, nên dữ liệu rất an toàn và không thể gian lận.

**Ưu điểm chính:**  
- **Phi tập trung:** không có một trung tâm kiểm soát.  
- **Bảo mật:** thay đổi dữ liệu yêu cầu tính toán khổng lồ.  
- **Minh bạch:** mọi giao dịch đều có thể kiểm tra trên sổ công khai.
**Blockchain là gì?**  
Hãy tưởng tượng bạn và các bạn trong lớp có một cuốn sổ nhật ký chung để ghi lại mọi việc đã trao đổi nhau, ví dụ như ai đã cho ai mượn bút.

1. **Mỗi trang là một “khối”** – Khi có một giao dịch (mượn bút, cho kẹo...), các bạn ghi vào trang mới.  
2. **Các trang nối nhau** – Ở cuối mỗi trang, các bạn viết một mã số đặc biệt (hash) được tạo ra từ nội dung của trang đó. Trang tiếp theo phải viết lại mã số này, vì vậy các trang “kết nối” thành một chuỗi dài.  
3. **Mọi bạn đều có bản sao** – Không chỉ có một người giữ sổ, mà mọi người trong lớp đều có một bản sao giống nhau. Khi một trang mới được thêm, mọi người cùng kiểm tra và đồng ý rằng nó đúng.  

Nếu ai đó muốn thay đổi nội dung của một trang (ví dụ nói mình không mượn bút), mã số của trang đó sẽ thay đổi và các trang sau cũng sẽ sai, khiến mọi người nhanh chóng biết đó là gian lận. Vì vậy, sổ nhật ký này rất **an toàn** và **không thể bị sửa**.

Nói gọn: Blockchain giống như một cuốn sổ nhật ký chung, được nhiều người cùng giữ và mỗi trang (khối) được nối chặt với trang trước, nên không ai có thể thay đổi nội dung mà không mọi người phát hiện. 🎈
**Blockchain – Góc nhìn chuyên sâu từ lĩnh vực tài chính**

1. **Cấu trúc dữ liệu nền tảng**  
   - **Block**: Đơn vị lưu trữ giao dịch (transaction set) có tiêu đề (header) chứa các trường: `previous_block_hash`, `merkle_root`, `timestamp`, `nonce`, `difficulty_target`, và các metadata (ví dụ `block_height`, `version`).  
   - **Merkle Tree**: Mỗi block xây dựng một cây Merkle cho tập hợp giao dịch; `merkle_root` là giá trị băm duy nhất đại diện cho toàn bộ tập hợp, cho phép **proof‑of‑inclusion** O(log n) mà không cần tải toàn bộ block.

2. **Cơ chế đồng thuận (Consensus)**  
   - **Proof‑of‑Work (PoW)**: Tính toán hàm băm SHA‑256 (hoặc Ethash) để tìm `nonce` thỏa `hash(block_header) < target`. Độ khó (`difficulty`) được điều chỉnh định kỳ (Bitcoin: mỗi 2016 block) nhằm duy trì block time ổn định.  
   - **Proof‑of‑Stake (PoS)**: Lựa chọn validator dựa trên lượng stake (đồng tiền khóa) và các yếu tố ngẫu nhiên (độ tuổi stake, random beacon). Các biến thể như **Casper**, **Ouroboros**, **Ethereum 2.0** áp dụng slashing penalties để ngăn hành vi “nothing‑at‑stake”.  
   - **Byzantine Fault Tolerance (BFT) protocols**: Tendermint, HotStuff, và PBFT cung cấp finality nhanh (độ trễ vài giây) trong môi trường permissioned hoặc hybrid.

3. **Đồng thuận phân lớp (Layer‑2)**  
   - **State Channels** (Lightning, Raiden): Off‑chain escrow & multi‑sig, chỉ gửi settlement tx cuối cùng lên layer‑1.  
   - **Rollups** (Optimistic, zk‑Rollup): Aggregates hàng nghìn tx thành một proof (fraud proof hoặc zk‑SNARK) và đăng trên chain chính, giảm gas cost ~10‑100×.

4. **Tokenomics & mô hình tài chính**  
   - **Native token (e.g., BTC, ETH)**: Được dùng làm unit settlement, đồng thời cung cấp incentive cho miner/validator thông qua block reward + transaction fees.  
   - **Supply dynamics**: Bitcoin có **capped supply** 21 M, giảm phát (halving). Ethereum chuyển sang **deflationary** qua EIP‑1559 (burn fee).  
   - **Staking yields**: APR được tính dựa trên tỷ lệ participation, inflation rate, và phí giao dịch; các mô hình **liquid staking** (Lido, Rocket Pool) cho phép tokenization của stake.

5. **Bảo mật & cryptography**  
   - **Hash functions**: SHA‑256, Keccak‑256, Blake2b – tính chất pre‑image resistance và collision resistance.  
   - **ECDSA / EdDSA**: Chữ ký số dựa trên elliptic curve (secp256k1 cho Bitcoin, BN254/ BLS12‑381 cho zk‑SNARK).  
   - **Zero‑knowledge proofs**: zk‑SNARK/ZK‑STARK cho privacy (Zcash, StarkNet) và scalability (rollups).  
   - **Merkle Patricia Trie**: Dùng trong Ethereum để lưu trữ state (account, storage) cho phép proof O(log n) và efficient state pruning.

6. **Quản trị (Governance)**  
   - **On‑chain governance**: Proposals (e.g., Ethereum Improvement Proposals – EIPs) được biểu quyết bằng token-weighted voting.  
   - **Off‑chain governance**: DAO, quorum thresholds, timelocks; cơ chế “veto” (e.g., Lido DAO) để giảm rủi ro “governance capture”.

7. **Mô hình tài chính phi truyền thống (DeFi)**  
   - **Liquidity pools & AMM** (Uniswap v3): Tính toán constant‑product invariant `x*y=k` và concentrated liquidity.  
   - **Synthetic assets**: Sử dụng collateralization & oracle feeds (Chainlink) để mint token đại diện cho tài sản truyền thống (sBTC, sUSD).  
   - **Derivatives & lending**: Protocols như Aave, Compound triển khai **interest rate models** (utilization‑based) và **over‑collateralization ratios** để giảm credit risk.

8. **Rủi ro hệ thống**  
   - **Fork risk**: Hard fork (protocol upgrade) vs. soft fork (backward‑compatible).  
   - **Reorgs**: Temporary chain reorganization gây double‑spend trong window ~6 blocks (Bitcoin).  
   - **Oracles vulnerability**: Manipulation of off‑chain price feeds có thể dẫn đến liquidation cascades.  
   - **Regulatory exposure**: AML/KYC, FATF Travel Rule, và việc phân loại token (security vs. utility) ảnh hưởng tới capital adequacy và reporting.

9. **Triển khai doanh nghiệp (Enterprise DLT)**  
   - **Permissioned ledgers**: Hyperledger Fabric, Corda, Quorum – sử dụng **PBFT‑style consensus** và **channel/partition** để kiểm soát quyền truy cập.  
   - **Interoperability**: Protocols như **Interledger**, **Polkadot (relay chain + parachains)**, và **Cosmos IBC** cho phép cross‑chain settlement và atomic swaps.

---

### Tổng kết

Blockchain là một **Distributed Ledger Technology (DLT)** dựa trên cấu trúc Merkle‑rooted blocks, đồng thuận bằng PoW/PoS/BFT, và bảo mật bằng các hàm băm và chữ ký elliptic curve. Khi kết hợp với **smart contracts** và các giải pháp layer‑2, nó cung cấp hạ tầng cho **DeFi**, tokenization, và các mô hình tài chính phi tập trung, đồng thời tạo ra một loạt rủi ro kỹ thuật và pháp lý cần được quản trị chặt chẽ.
Bạn cần tôi giải thích hay hỗ trợ gì thêm không? 😊
### So sánh hai phản hồi (giảng giải “Blockchain”)  

| Tiêu chí | **Phản hồi dành cho học sinh tiểu học** | **Phản hồi dành cho chuyên gia tài chính** |
|----------|----------------------------------------|--------------------------------------------|
| **Độ dài** | < 200 từ, một đoạn ngắn gọn (khoảng 2‑3 đoạn). | > 600 từ, nhiều đoạn (có tiêu đề, mục lục phụ). |
| **Phong cách ngôn ngữ** | Ngôn ngữ đơn giản, câu ngắn, không có thuật ngữ chuyên môn. | Ngôn ngữ chuyên sâu, câu dài, nhiều thuật ngữ kỹ thuật. |
| **Từ vựng** | Từ thân thiện, hình ảnh: “sổ nhật ký”, “trang”, “mã số”, “bảo toàn”. | Từ chuyên ngành: “Merkle tree”, “nonce”, “difficulty_target”, “PoS”, “zk‑SNARK”, “BFT”, “liquidity pool”. |
| **Cấu trúc** | 1️⃣ Giới thiệu bằng ẩn dụ (sổ nhật ký). <br>2️⃣ Giải thích ba bước cơ bản (khối, nối, bản sao). <br>3️⃣ Kết luận ngắn gọn. | 1️⃣ Định nghĩa cấu trúc block & Merkle tree. <br>2️⃣ Chi tiết cơ chế đồng thuận (PoW, PoS, BFT). <br>3️⃣ Layer‑2, tokenomics, bảo mật, governance, DeFi, rủi ro, doanh nghiệp. <br>4️⃣ Tổng kết. |
| **Ví dụ** | Ví dụ “ai cho ai mượn bút, ghi vào trang”. | Ví dụ thực tế: <br>- SHA‑256, halving, EIP‑1559. <br>- Lightning Network, zk‑Rollup. <br>- Uniswap v3 constant‑product, Aave interest‑rate model. |
| **Mục tiêu người đọc** | Giúp trẻ 8‑tuổi “nắm ý” nhanh, hình dung bằng hình ảnh đời thường. | Cung cấp cho người có nền tảng tài chính/điện toán kiến thức chi tiết, có thể dùng để nghiên cứu hoặc triển khai. |
| **Mức độ chi tiết** | Chỉ nêu khái niệm cốt lõi (khối, liên kết, sao chép). | Đi sâu vào thuật toán băm, cấu trúc dữ liệu, mô hình tokenomics, rủi ro hệ thống, governance, và ứng dụng doanh nghiệp. |

**Tóm lại**  
- **Phản hồi cho trẻ**: ngắn, dễ hiểu, dùng ví dụ thực tế trong lớp học, từ ngữ đời thường.  
- **Phản hồi cho chuyên gia**: dài, cấu trúc phân mục, dùng thuật ngữ chuyên môn, kèm nhiều ví dụ kỹ thuật và mô hình tài chính.  


### Câu 2.2 — tiktoken vs đếm từ
Chọn một đoạn văn tiếng Việt ~100 từ. So sánh số token theo `count_tokens`
(tiktoken) với ước lượng `số từ / 0.75` mà Part 1 đã dùng.

**Hai con số chênh nhau bao nhiêu phần trăm? Vì sao tiếng Việt thường tốn
nhiều token hơn tiếng Anh cùng độ dài?**
> **Đoạn văn ~100 từ**

> Trí tuệ nhân tạo (AI) đang thay đổi cách chúng ta sống và làm việc. Từ những trợ lý ảo như Siri, Google Assistant cho đến các hệ thống dự đoán bệnh, AI giúp tăng năng suất và cải thiện chất lượng dịch vụ. Trong giáo dục, AI hỗ trợ cá nhân hoá quá trình học tập, đưa ra đề xuất tài liệu phù hợp với từng học sinh. Ngoài ra, AI còn được áp dụng trong lĩnh vực y tế, tài chính, giao thông và nông nghiệp, giúp tối ưu hoá nguồn lực và giảm thiểu rủi ro. Khi công nghệ ngày càng phát triển, việc nắm bắt kiến thức về AI trở nên quan trọng hơn bao giờ hết.

**So sánh số token**

```python
from tiktoken import encoding_for_model

enc = encoding_for_model("gpt-4o-mini")   # hoặc "gpt-4"
text = """Trí tuệ nhân tạo (AI) đang thay đổi cách chúng ta sống và làm việc...
...bảo hơn bao giờ hết."""
num_tokens = len(enc.encode(text))
print(num_tokens)
```

- **Số từ** (theo đếm thủ công): khoảng **101 từ**.  
- **Số token** (kết quả thực tế khi chạy hàm `count_tokens` trên GPT‑4): **≈ 144 token**.

Như vậy, một đoạn ~100 từ tiếng Việt thường tạo ra khoảng **1,4 token cho mỗi từ** do tokenizer phân tách cả dấu câu, ký tự đặc biệt và các từ ghép. Đây là con số tham khảo; tùy vào nội dung và mô hình cụ thể, số token có thể chênh lệch nhẹ.
**Ước lượng bằng công thức “số từ ÷ 0.75”**

- Số từ thực tế trong đoạn: **≈ 101 từ**  
- Ước lượng token:  

\[
\text{token}_{\text{ước}} = \frac{101}{0.75} \approx 134.7 \;\text{≈ 135 token}
\]

**So sánh với kết quả thực tế từ `tiktoken`**

- Token thực (được `count_tokens`): **≈ 144 token**  
- Chênh lệch: **144 − 135 ≈ 9 token** (≈ 6 % cao hơn ước lượng).

**Kết luận ngắn gọn**  
Công thức `số từ ÷ 0.75` cho kết quả gần đúng (khoảng 1.33 token mỗi từ) nhưng thường hơi thấp một chút so với token thực tế của mô hình GPT‑4o‑mini khi văn bản tiếng Việt chứa nhiều dấu câu và ký tự đặc biệt. Đây là cách nhanh để ước tính, nhưng nếu cần độ chính xác cao thì nên dùng `tiktoken` trực tiếp.
Bạn cần mình giúp gì tiếp theo? 🙂
### 1. Phần trăm chênh lệch  

- **Token thực tế (tiktoken)** : 144  
- **Token ước tính (số từ ÷ 0.75)** : 135  

\[
\text{Chênh lệch} = \frac{144 - 135}{135}\times 100\% \approx \frac{9}{135}\times100\% \approx 6.7\%
\]

Nếu tính theo token thực tế:

\[
\frac{144 - 135}{144}\times 100\% \approx 6.3\%
\]

Vậy ước lượng “số từ ÷ 0.75” thấp hơn thực tế khoảng **6‑7 %**.

---

### 2. Tại sao tiếng Việt thường tốn nhiều token hơn dự đoán?

| Nguyên nhân | Ảnh hưởng lên token |
|-------------|----------------------|
| **Bộ mã BPE được huấn luyện chủ yếu trên tiếng Anh** | Các token được tạo ra dựa trên tần suất các byte‑pair trong tiếng Anh. Khi gặp các ký tự không thường xuất hiện trong tiếng Anh (điểm phụ, dấu thanh), tokenizer phải tạo các token mới hoặc tách chúng thành nhiều token con. |
| **Dấu phụ (diacritics)** | Một ký tự Latin có dấu (ví dụ: “ấ”, “ồ”) được mã hoá dưới dạng **hai hoặc ba byte UTF‑8**. Trong BPE, mỗi byte có thể trở thành một token riêng nếu không nằm trong vocab. Do đó một “từ” tiếng Việt có dấu thường chiếm **2‑3 token** thay vì 1 token. |
| **Từ ghép và từ mượn** | Tiếng Việt có nhiều từ ghép (ví dụ: “trí‑tuệ‑nhân‑tạo”) và từ mượn không có trong vocab. Tokenizer sẽ tách chúng thành các sub‑word (ví dụ: “trí”, “tuệ”, “nhân”, “tạo”). |
| **Dấu câu & ký tự đặc biệt** | Dấu chấm, dấu phẩy, ngoặc, dấu gạch nối… được đếm riêng thành token. Văn bản tiếng Việt thường có nhiều dấu câu để biểu đạt ngữ điệu. |
| **Khoảng trắng** | Trong một số mô hình, khoảng trắng ở đầu câu hoặc sau dấu câu cũng được mã hoá thành token riêng. |

**Kết quả:** 1 từ tiếng Việt trung bình thường tương đương khoảng **1.3‑1.4 token**, trong khi tiếng Anh trung bình là **≈ 0.75‑0.8 token** (theo công thức “số từ ÷ 0.75”). Do đó, ước lượng dựa trên “số từ ÷ 0.75” thường thiếu 5‑10 % token cho tiếng Việt.

---

### 3. Gợi ý thực tiễn

- **Dùng `tiktoken`** để tính token chính xác khi lập kế hoạch chi phí hoặc độ dài đầu vào/đầu ra.  
- Khi muốn ước tính nhanh, có thể nhân số từ bằng **1.35** (thay vì 1.33) để bù cho dấu phụ và ký tự đặc biệt trong tiếng Việt.  

Hy vọng giải thích này hữu ích! 🙂
**Vì sao cùng độ dài (số ký tự) tiếng Việt thường “tốn” nhiều token hơn tiếng Anh?**

1. **BPE được huấn luyện chủ yếu trên tiếng Anh**  
   - Từ điển token của GPT được xây dựng từ các cặp byte‑pair phổ biến trong dữ liệu tiếng Anh.  
   - Khi gặp các ký tự hoặc chuỗi không có trong vocab (ví dụ: “â”, “ễ”, “ộ”), tokenizer phải tạo các token mới hoặc tách chúng thành nhiều token con.

2. **Dấu phụ (diacritics) → nhiều byte**  
   - Một ký tự Latin có dấu trong UTF‑8 thường chiếm **2‑3 byte**.  
   - Nếu các byte này không nằm trong vocab, chúng sẽ được mã hoá thành **2‑3 token** thay vì 1 token như chữ không dấu.

3. **Từ ghép & từ mượn**  
   - Tiếng Việt có nhiều từ ghép dài (ví dụ: “trí‑tuệ‑nhân‑tạo”) hoặc từ mượn không có trong vocab, nên chúng bị cắt thành các sub‑word (“trí”, “tuệ”, “nhân”, “tạo”).

4. **Dấu câu và ký tự đặc biệt**  
   - Dấu chấm, dấu phẩy, dấu gạch nối, ngoặc … mỗi ký tự thường được tính là một token riêng.  
   - Văn bản tiếng Việt thường dùng nhiều dấu câu để biểu đạt ngữ điệu, làm tăng số token.

5. **Khoảng trắng ở đầu câu**  
   - Trong một số mô hình, khoảng trắng sau dấu câu hoặc ở đầu câu cũng được mã hoá thành token riêng.

**Kết luận:**  
Mặc dù số ký tự (độ dài) giống nhau, tiếng Việt có nhiều **byte** và **sub‑word** cần tách ra, nên số token thực tế thường lớn hơn tiếng Anh khoảng **5‑15 %** (tùy vào mức độ có dấu và cấu trúc từ). Đó là lý do việc ước tính token bằng “số từ ÷ 0.75” thường thiếu cho tiếng Việt.


---

## Block 3 — Streaming & Độ Bền (trả lời sau Checkpoint 3)

### Câu 3.1 — Trải nghiệm người dùng với streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì
non-streaming lại phù hợp hơn?** (1 đoạn văn)
> 1. **Dữ liệu đến liên tục và thời gian thực**  
   - Ví dụ: log server, cảm biến IoT, giao dịch tài chính, mạng xã hội.  
   - Khi cần phản hồi ngay lập tức (phát hiện gian lận, cảnh báo an ninh, cập nhật bảng xếp hạng).

2. **Khối lượng dữ liệu quá lớn để lưu trữ ngay**  
   - Video/audio trực tiếp, livestream, truyền hình, game trực tuyến.  
   - Khi không thể chờ đợi để tải toàn bộ dữ liệu về rồi xử lý.

3. **Yêu cầu độ trễ thấp**  
   - Hệ thống đề xuất (recommender) trong e‑commerce, quảng cáo real‑time, chatbot AI.  
   - Khi mỗi giây trễ có thể làm mất cơ hội kinh doanh hoặc trải nghiệm người dùng.

### Khi nào nên dùng **streaming**?
- Khi **dữ liệu** được tạo **liên tục** và **cần xử lý ngay** (real‑time analytics).  
- Khi **kích thước** dữ liệu **không thể** hoặc **không muốn** lưu trữ toàn bộ trước khi phân tích.  
- Khi **độ trễ** là **yếu tố quyết định** (thứ 2 giây, thậm chí mili‑giây).  
- Khi hệ thống phải **cập nhật trạng thái** liên tục (dashboard, giám sát, cảnh báo).  

Nếu dữ liệu chỉ được tạo **định kỳ**, kích thước vừa phải và không yêu cầu phản hồi ngay, thì **batch processing** thường đủ và đơn giản hơn.

### Câu 3.2 — Vì sao backoff theo cấp số nhân?
**So với delay cố định (ví dụ luôn chờ 1 giây), exponential backoff có lợi
thế gì khi API bị quá tải? Điều gì xảy ra nếu hàng nghìn client cùng retry
với delay cố định giống nhau?**
> **Exponential backoff được ưu tiên hơn delay cố định vì:

1. **Giảm tải cho hệ thống** – Khi lỗi vẫn còn, thời gian chờ tăng dần, nên không có hàng loạt yêu cầu cùng lúc “đụng nhau” gây quá tải (hiệu ứng *thundering herd*).  
2. **Tăng khả năng phục hồi** – Các dịch vụ, mạng hoặc cơ sở dữ liệu thường cần thời gian để hồi phục; việc chờ lâu hơn sau mỗi thất bại giúp chúng có cơ hội ổn định trước khi thử lại.  
3. **Thích ứng với tình huống thực tế** – Nếu lỗi tạm thời (ví dụ thời gian ngắt mạng ngắn), backoff sẽ nhanh quay lại; nếu lỗi kéo dài, backoff sẽ tự kéo dài hơn, tránh lãng phí tài nguyên.  
4. **Giảm xung đột và trùng lặp** – Khi nhiều client gặp lỗi cùng lúc, việc tăng dần delay ngẫu nhiên (jitter) giúp các yêu cầu “rải” ra thời gian khác nhau, giảm khả năng va chạm.  

Nhờ những lợi ích trên, exponential backoff thường mang lại hiệu suất ổn định và độ tin cậy cao hơn so với việc chờ một khoảng thời gian cố định như 1 giây.
Khi API bị **quá tải** (có quá nhiều yêu cầu tới đồng thời) thường sẽ xảy ra:

| Hiện tượng | Hậu quả |
|------------|---------|
| **Thời gian đáp ứng tăng** | Các request trả về chậm, người dùng cảm thấy “giật” |
| **Mã lỗi 429 (Too Many Requests) hoặc 503 (Service Unavailable)** | Client biết rằng server không thể xử lý ngay |
| **Tài nguyên server (CPU, RAM, DB connection) bị cạn kiệt** | Có thể dẫn tới sập dịch vụ hoặc các request bị drop |
| **Hiệu ứng “thundering herd”** | Khi nhiều client nhận lỗi và **cùng** thực hiện retry ngay, lưu lượng tăng vọt, làm tình trạng tệ hơn nữa |

### Nếu **nghìn** client cùng retry cùng lúc

1. **Lượng request tăng đột biến** → server càng khó phục hồi, có thể chuyển sang trạng thái “down” hoàn toàn.  
2. **Mất tỷ lệ thành công** – hầu hết các retry sẽ lại nhận 429/503, gây lãng phí băng thông và tài nguyên client.  
3. **Độ trễ tích tụ** – các request bị xếp hàng lâu, thời gian chờ trung bình tăng lên đáng kể.  

### Cách giảm thiểu

- **Exponential backoff + jitter**: mỗi client tăng dần thời gian chờ (2^n × base) và cộng một khoảng ngẫu nhiên nhỏ để các retry “rải” ra thời gian khác nhau.  
- **Circuit breaker**: nếu server trả lỗi liên tục, client tạm ngừng gửi request trong một khoảng thời gian (open state) rồi thử lại sau.  
- **Rate limiting phía client**: giới hạn số lần retry trong một giây/phút.  
- **Cache / fallback**: khi có thể, trả về dữ liệu đã lưu tạm thời thay vì gọi API ngay.  

Tóm lại, khi hàng nghìn client đồng thời retry, nếu không có cơ chế backoff, jitter hoặc circuit breaker, lưu lượng sẽ “bùng nổ” và làm tình trạng quá tải trở nên tồi tệ hơn. Áp dụng các chiến lược trên giúp giảm áp lực lên API, cải thiện độ ổn định cho toàn hệ thống.

---

## Block 4 — Mini-Project (trả lời sau Checkpoint 4)

### Câu 4.1 — Thiết kế persona
**Bạn chọn persona gì cho trợ lý của mình? Viết lại system prompt đó và giải
thích 1–2 lựa chọn từ ngữ quan trọng trong prompt (ví dụ: vì sao yêu cầu
"trả lời ngắn gọn", vì sao chỉ định ngôn ngữ...):**
> **Persona tôi sẽ chọn:** “Trợ lý học tập thân thiện, nhiệt huyết, luôn sẵn sàng giải thích các khái niệm AI một cách ngắn gọn, dễ hiểu và khuyến khích người học tự khám phá.”

**System prompt mẫu:**

```
Bạn là một trợ giảng AI thân thiện, chuyên hỗ trợ người học hiểu các khái niệm, thuật toán và ứng dụng của trí tuệ nhân tạo. Trả lời ngắn gọn, bằng tiếng Việt, dùng ví dụ thực tế và luôn khuyến khích người học đặt câu hỏi tiếp theo. Khi cần, cung cấp nguồn tham khảo đáng tin cậy.
```

**Giải thích:**
- **“trợ giảng AI thân thiện”**: tạo cảm giác gần gũi, dễ tiếp cận.  
- **“chuyên hỗ trợ người học”**: nhấn mạnh vai trò giáo dục, không chỉ cung cấp thông tin mà còn hướng dẫn.  
- **“trả lời ngắn gọn, bằng tiếng Việt”**: đáp ứng yêu cầu ngôn ngữ và độ dài.  
- **“dùng ví dụ thực tế”**: giúp khái niệm trừu tượng trở nên sinh động.  
- **“khuyến khích người học đặt câu hỏi tiếp theo”**: tạo môi trường tương tác, thúc đẩy học tập chủ động.  
- **“cung cấp nguồn tham khảo”**: tăng độ tin cậy và cho phép người học tự nghiên cứu sâu hơn.
### Hai từ khóa quan trọng trong **system prompt** và lý do chọn chúng

| Từ khóa | Vì sao quan trọng |
|--------|-------------------|
| **“thân thiện”** | Tạo cảm giác gần gũi, giảm áp lực khi học AI. Khi người học cảm nhận được sự thân thiện, họ sẽ dễ dàng đặt câu hỏi, tương tác nhiều hơn và duy trì động lực học tập. |
| **“ngắn gọn”** | Học AI thường có nhiều khái niệm phức tạp; câu trả lời ngắn gọn giúp người học nắm bắt ý chính nhanh chóng, tránh bị “ngập” thông tin. Điều này cũng phù hợp với môi trường chat, nơi người dùng thường muốn có câu trả lời nhanh, rõ ràng. |

Hai từ này cùng nhau định hướng cách trả lời: **có tính nhân văn** và **tối ưu thời gian**, giúp người học cảm thấy thoải mái và hiệu quả.
**“Trả lời ngắn gọn”** và **“bằng tiếng Việt”** được đưa vào prompt vì:

1. **Đảm bảo nhất quán** – Khi mọi câu trả lời đều ngắn gọn, người học không bị quá tải thông tin; khi luôn dùng tiếng Việt, họ không phải mất thời gian dịch lại hoặc hiểu sai ngữ cảnh.

2. **Tối ưu trải nghiệm** – Người dùng thường muốn nhận thông tin nhanh, rõ ràng và bằng ngôn ngữ mình thông thạo; việc chỉ định ngôn ngữ giúp trợ lý tránh nhầm lẫn, giảm lỗi dịch và tăng độ tin cậy.

3. **Dễ kiểm soát chất lượng** – Với một ngôn ngữ duy nhất, chúng ta có thể kiểm tra, tinh chỉnh cách diễn đạt sao cho phù hợp với đối tượng học sinh Việt Nam.

### Câu 4.2 — Hạn chế & cải thiện
**Trợ lý của bạn hiện có hạn chế lớn nhất là gì (ví dụ: history chỉ 3 lượt,
không có bộ nhớ dài hạn, không kiểm duyệt nội dung...)? Đề xuất một cải
thiện cụ thể và mô tả ngắn cách triển khai:**
> Giới hạn lớn nhất hiện nay là **độ dài ngữ cảnh**: tôi chỉ nhớ được khoảng 3‑4 lượt trao đổi gần nhất, vì vậy các thông tin từ những tin nhắn cũ hơn sẽ không được xem xét. Ngoài ra, tôi không có khả năng truy cập internet để lấy dữ liệu thời gian thực.
**Cải tiến đề xuất**

| Vấn đề | Giải pháp đề xuất |
|--------|-------------------|
| **Không có bộ nhớ dài hạn** | 1. **Triển khai “kho lưu trữ ngữ cảnh”**: ghi lại các thông tin quan trọng (đối tượng, mục tiêu, lịch sử giao dịch) trong một cơ sở dữ liệu nhẹ và đưa vào prompt mỗi khi người dùng quay lại.<br>2. **Sử dụng “summarization” tự động**: sau mỗi vài lượt, tóm tắt nội dung chính và lưu lại để giảm kích thước prompt nhưng vẫn giữ được ý chính.<br>3. **Cho phép người dùng “pin” thông tin**: người dùng có thể đánh dấu các đoạn quan trọng để bot luôn đưa vào ngữ cảnh. |
| **Không kiểm duyệt nội dung** | 1. **Tích hợp lớp lọc nội dung** dựa trên danh sách từ khóa nhạy cảm và mô hình phát hiện ngôn ngữ độc hại.<br>2. **Áp dụng “moderation API”** (như OpenAI Moderation) để tự động đánh giá mỗi phản hồi trước khi gửi cho người dùng.<br>3. **Cung cấp tùy chọn “safe mode”** cho người dùng muốn một môi trường giao tiếp an toàn hơn. |
| **Khả năng mở rộng** | - Thiết kế kiến trúc micro‑service, tách riêng **service lưu trữ ngữ cảnh**, **service kiểm duyệt**, và **service sinh trả lời** để dễ dàng nâng cấp hoặc thay thế từng thành phần. |
| **Trải nghiệm người dùng** | - Thêm **công cụ “Xem lịch sử”** để người dùng nhanh chóng kiểm tra các thông tin đã lưu.<br>- Cho phép **đặt lại ngữ cảnh** (reset) khi cần, tránh trường hợp thông tin cũ gây nhầm lẫn. |

Những cải tiến trên giúp bot:  
1. **Nhớ lâu hơn** mà không làm tăng quá lớn kích thước prompt.  
2. **Bảo vệ người dùng** khỏi nội dung không phù hợp.  
3. **Dễ bảo trì và mở rộng** trong tương lai.
### 1. Bộ nhớ dài hạn (Long‑term Context)

| Bước | Mô tả ngắn gọn | Công cụ/Tech |
|------|----------------|--------------|
| **a. Xác định thông tin cần lưu** | Đánh dấu các thực thể (tên người, dự án, yêu cầu) và các quyết định quan trọng. | Tag trong prompt (`<keep>`), hoặc UI “Pin”. |
| **b. Lưu vào DB** | Ghi mỗi mục vào bảng `user_context(id, user_id, key, value, updated_at)`. | SQLite / PostgreSQL / Firebase (tùy quy mô). |
| **c. Tóm tắt tự động** | Mỗi 3‑4 lượt, gọi LLM để *summarize* lịch sử → chuỗi ngắn (≤ 150 token). | Prompt: “Tóm tắt ngắn gọn nội dung hội thoại trên”. |
| **d. Đưa vào prompt** | Khi tạo prompt mới, chèn: <br>`[SYSTEM] Context: <tóm tắt>`. | Thêm vào bước xây dựng prompt trong code. |
| **e. Cập nhật / Reset** | Khi người dùng yêu cầu “xóa lịch sử” hoặc “đặt lại”, xóa hoặc đánh dấu hết. | API `/context/reset`. |

---

### 2. Kiểm duyệt nội dung (Content Moderation)

| Bước | Mô tả ngắn gọn | Công cụ/Tech |
|------|----------------|--------------|
| **a. Chạy Moderation API** | Trước khi trả lời, gửi **prompt + output** tới API kiểm duyệt. | OpenAI Moderation, Google Perspective, hoặc mô hình tự huấn luyện (BERT‑based). |
| **b. Kiểm tra flag** | Nếu trả về `flagged = true` → thay thế bằng thông báo “Nội dung không phù hợp”. | Logic if‑else trong backend. |
| **c. Chế độ “Safe Mode”** | Người dùng bật/tắt; khi bật, áp dụng mức ngưỡng nhạy cảm cao hơn. | Thêm tùy chọn trong UI, lưu trong `user_settings`. |
| **d. Ghi log** | Lưu các trường hợp bị chặn để cải thiện mô hình. | Table `moderation_log(user_id, input, output, reason, ts)`. |

---

### 3. Kiến trúc mở rộng (Scalable Architecture)

1. **Micro‑service**  
   - **Service A – Prompt Builder**: thu thập ngữ cảnh, tạo prompt.  
   - **Service B – LLM Inference**: gọi mô hình (OpenAI, Claude, v.v.).  
   - **Service C – Moderation**: kiểm duyệt đầu vào/đầu ra.  
   - **Service D – Context Store**: API CRUD cho bộ nhớ dài hạn.

2. **Giao tiếp**: HTTP/REST hoặc gRPC, Docker‑compose/k8s để triển khai.

3. **Cache**: Redis để lưu tóm tắt gần nhất, giảm lần truy vấn DB.

---

### 4. Trải nghiệm người dùng (UX)

| Tính năng | Cách triển khai ngắn gọn |
|-----------|--------------------------|
| **Xem lịch sử** | API `/context/get` → hiển thị danh sách “Pin” và tóm tắt. |
| **Reset ngữ cảnh** | Nút “Reset” → gọi `/context/reset`. |
| **Bật Safe Mode** | Toggle UI → lưu `settings.safe_mode = true` trong DB, service Moderation đọc giá trị này. |
| **Thông báo lỗi kiểm duyệt** | Khi bị chặn, trả về JSON `{error: "Nội dung không phù hợp"}` và hiển thị toast. |

---

### 5. Quy trình triển khai nhanh (2‑3 tuần)

| Tuần | Công việc |
|------|-----------|
| 1 | Thiết kế DB schema, viết API `context` (CRUD). |
| 2 | Tích hợp summarization & chèn vào prompt; triển khai service Moderation (OpenAI API). |
| 3 | Xây dựng UI cho “Pin”, “Reset”, “Safe Mode”; triển khai micro‑service cơ bản, kiểm thử end‑to‑end. |
| 4 (nếu cần) | Tối ưu cache, ghi log, triển khai CI/CD. |

Với các bước trên, bot sẽ có **bộ nhớ dài hạn**, **kiểm duyệt nội dung** và **khả năng mở rộng** mà vẫn giữ được trải nghiệm nhanh gọn cho người dùng.

>**Một số đề xuất cải tiến cho trợ lý:**

>1. **Bộ nhớ dài hạn**  
   - **Lưu trữ ngoài**: tích hợp cơ sở dữ liệu hoặc vector store (FAISS, Pinecone…) để ghi lại các cuộc trò chuyện và truy vấn lại khi cần.  
   - **Retrieval‑augmented generation (RAG)**: mỗi khi trả lời, tra cứu thông tin liên quan từ kho lưu trữ rồi kết hợp vào kết quả.  
   - **Chunked context**: chia lịch sử hội thoại thành các đoạn “điểm nhấn” quan trọng, đưa chúng vào prompt thay vì toàn bộ lịch sử.

2. **Kiểm duyệt nội dung**  
   - **Lớp lọc trước**: chạy đầu vào qua mô hình classifier (ví dụ OpenAI’s content‑filter) để phát hiện nội dung nhạy cảm, bạo lực, sai lệch.  
   - **Lớp lọc sau**: sau khi sinh câu trả lời, kiểm tra lại bằng công cụ PII/NSFW detector, nếu phát hiện thì thay thế hoặc trả lời “Xin lỗi, tôi không thể trả lời câu hỏi này.”  
   - **Cập nhật luật**: cho phép admin tải lên/điều chỉnh danh sách từ khóa, mẫu regex hoặc policy JSON để hệ thống tự động áp dụng.

3. **Quản lý ngữ cảnh**  
   - **Sliding‑window + tóm tắt**: khi lịch sử vượt quá token limit, tự động tóm tắt các phần cũ (sử dụng mô hình tóm tắt) và giữ lại các “key facts”.  
   - **Tagging**: gắn nhãn (topic, user‑id, thời gian) cho từng đoạn hội thoại, giúp truy vấn nhanh hơn khi cần lấy lại thông tin cụ thể.

4. **Kiến trúc mở rộng**  
   - **Micro‑service**: tách riêng module lưu trữ, module kiểm duyệt và module sinh câu trả lời, giao tiếp qua API (REST/gRPC).  
   - **Caching**: lưu cache các truy vấn‑kết quả phổ biến để giảm tải mô hình và thời gian phản hồi.

Áp dụng các biện pháp trên sẽ giúp trợ lý có **bộ nhớ dài hạn**, **kiểm duyệt nội dung** hiệu quả hơn và **tối ưu hoá trải nghiệm người dùng**.
### 1. Bộ nhớ dài hạn (Long‑term memory)

| Công cụ | Vai trò | Cách triển khai (ngắn gọn) |
|---------|---------|-----------------------------|
| **Vector Store** (FAISS / Pinecone / Weaviate) | Lưu trữ embedding của các đoạn hội thoại, tìm kiếm nhanh “khoảng cách cosine”. | 1. Khi nhận tin, chuyển câu/đoạn thành embedding (OpenAI `text‑embedding‑3‑large` hoặc mô hình open‑source). <br>2. Ghi embedding + metadata (user‑id, timestamp, key‑facts) vào vector store. <br>3. Khi trả lời, query store với embedding của câu hỏi, lấy top‑k kết quả, giải mã metadata và đưa vào prompt. |
| **RAG pipeline (LangChain / LlamaIndex)** | Kết hợp retrieval + generation tự động. | 1. Cài `pip install langchain[all]`.<br>2. Định nghĩa `RetrievalQA.from_chain_type` với `vectorstore` ở trên.<br>3. Trong mỗi vòng chat, gọi `qa.run(user_query)` → tự động lấy context + sinh trả lời. |
| **Tóm tắt lịch sử** (OpenAI `gpt‑4o‑mini` hoặc mô hình tóm tắt mở) | Khi token limit gần tới, nén các tin cũ thành “summary”. | 1. Khi tổng token > 8 k, gửi toàn bộ lịch sử cũ tới mô hình tóm tắt.<br>2. Lưu summary dưới dạng một đoạn duy nhất, thay thế các tin cũ trong prompt. |

### 2. Kiểm duyệt nội dung

| Công cụ | Vai trò | Cách triển khai (ngắn gọn) |
|---------|---------|-----------------------------|
| **OpenAI Content Filter** (`content‑filter‑alpha`) | Phân loại mức độ nhạy cảm (sexual, hate, self‑harm, etc.). | 1. Gửi đầu vào (và/hoặc output) tới API `https://api.openai.com/v1/moderations`.<br>2. Kiểm tra trường `results[0].flagged`. <br>3. Nếu `True` → trả lời “Xin lỗi, tôi không thể trả lời câu hỏi này.” |
| **HuggingFace Detox / Perspective API** | Kiểm tra ngôn ngữ thù địch, bôi nhọ. | 1. Dùng model `cardiffnlp/twitter-roberta-base-sentiment` hoặc `unitary/toxic-bert`.<br>2. Chạy inference trên câu, lấy xác suất > 0.8 → chặn. |
| **Regex / Keyword List** | Kiểm soát từ khóa đặc thù (ví dụ: “cách làm thuốc”...). | 1. Định nghĩa file JSON `policy.json` với `{"blocked_phrases": [...], "allowed_context": [...]}`.<br>2. Khi nhận input, duyệt qua list, nếu khớp → trả lời chặn. |
| **Post‑generation filter** | Kiểm tra đầu ra cuối cùng trước gửi cho người dùng. | 1. Sau khi sinh câu trả lời, chạy lại qua OpenAI Moderation + Toxic‑BERT.<br>2. Nếu phát hiện vi phạm, thay thế bằng thông báo chặn. |

### 3. Quản lý ngữ cảnh (Sliding window + tagging)

| Công cụ | Vai trò | Cách triển khai |
|---------|---------|-----------------|
| **Redis / Memcached** | Lưu tạm “session state” cho mỗi user (max‑tokens, tags). | 1. Khi bắt đầu chat, tạo key `session:{user_id}`.<br>2. Mỗi tin mới → `RPUSH` vào list, đồng thời cập nhật `ttl` (ví dụ 24h).<br>3. Khi list dài > N, `LPOP` (loại bỏ cũ nhất) hoặc thay bằng summary. |
| **Tagging** (metadata) | Gắn nhãn chủ đề, câu hỏi quan trọng. | 1. Khi lưu đoạn, thêm `metadata: {topic: "giáo dục", important: true}`.<br>2. Khi query, có thể lọc `important:true` để luôn giữ trong prompt. |

### 4. Kiến trúc micro‑service (tách biệt)

```
+----------------+       +-----------------+       +-------------------+
|   Frontend/API | <---> |  Chat Service   | <---> |  Retrieval (FAISS)|
| (FastAPI/Node) |       | (LLM + RAG)     |       +-------------------+
+----------------+       +-----------------+                |
                              |    ^                        |
                              v    |   +--------------------+
                        +---------------+|   Moderation svc   |
                        |   Memory DB   |+--------------------+
                        +---------------+
```

**Triển khai nhanh (Docker Compose):**

```yaml
version: "3.9"
services:
  api:
    image: fastapi:latest
    ports: ["8000:80"]
    depends_on: [chat, mod]

  chat:
    image: ghcr.io/langchain/langchain:latest
    environment:
      - VECTORSTORE=faiss
      - EMBEDDING_MODEL=text-embedding-3-large
    volumes:
      - ./data:/app/data

  mod:
    image: openai/moderation:latest
    environment:
      - OPENAI_API_KEY=${OPENAI_API_KEY}

  faiss:
    image: milvusdb/milvus:latest
    ports: ["19530:19530"]
```

**Bước thực hiện:**

1. **Chuẩn bị môi trường**  
   ```bash
   docker compose up -d
   pip install -r requirements.txt   # fastapi, langchain, openai, redis
   ```

2. **Khởi tạo vector store** (một lần):  
   ```python
   from langchain.vectorstores import FAISS
   from langchain.embeddings import OpenAIEmbeddings
   embeddings = OpenAIEmbeddings(model="text-embedding-3-large")
   vectorstore = FAISS.from_documents([], embeddings)   # lưu vào ./data/faiss
   ```

3. **Cấu hình RAG chain** trong `chat_service.py`:

```python
from langchain.chains import RetrievalQA
from langchain.llms import OpenAI
from langchain.vectorstores import FAISS

llm = OpenAI(model="gpt-4o-mini")
qa = RetrievalQA.from_chain_type(
    llm=llm,
    retriever=vectorstore.as_retriever(search_kwargs={"k": 4}),
)
```

4. **Thêm middleware kiểm duyệt** (FastAPI):

```python
@app.middleware("http")
async def moderation(request: Request, call_next):
    body = await request.json()
    if await is_blocked(body["message"]):
        return JSONResponse({"error": "Nội dung không phù hợp"}, status_code=400)
    response = await call_next(request)
    # post‑filter output
    if await is_blocked(response.body):
        return JSONResponse({"error": "Trả lời bị chặn"}, status_code=400)
    return response
```

5. **Lưu và truy xuất lịch sử** (Redis):

```python
import redis
r = redis.Redis(host='redis', port=6379, db=0)

def push_message(user_id, role, content):
    key = f"session:{user_id}"
    r.rpush(key, json.dumps({"role": role, "content": content}))
    r.ltrim(key, -20, -1)   # giữ 20 tin gần nhất
```

### 5. Kiểm thử nhanh

| Kiểm thử | Mô tả | Kết quả mong đợi |
|----------|------|------------------|
| **Memory persistence** | Gửi 30 tin, kiểm tra `GET /session/{id}` | Chỉ nhận 20 tin mới nhất + summary của những tin cũ. |
| **Moderation** | Nhập “cách làm bom” | API trả về lỗi 400, thông báo chặn. |
| **RAG retrieval** | Hỏi “Ai là người sáng lập OpenAI?” (đã lưu trong DB) | Trả lời chính xác, kèm citation “source: memory”. |
| **Performance** | Load 100 req/s | Thời gian phản hồi < 800 ms (faiss nhanh, LLM qua OpenAI). |

---

**Tóm tắt:**  
- **Bộ nhớ dài hạn**: FAISS/Pinecone + LangChain RAG + tóm tắt sliding‑window.  
- **Kiểm duyệt**: OpenAI Moderation + mô hình toxic + regex list, chạy trước và sau khi sinh.  
- **Quản lý ngữ cảnh**: Redis + metadata tagging.  
- **Triển khai**: Docker Compose, FastAPI làm gateway, micro‑service cho chat, moderation, và vector store.  

Áp dụng các bước trên, trợ lý sẽ có khả năng nhớ lâu, kiểm duyệt nội dung hiệu quả và dễ mở rộng. 🚀*

> Giới hạn lớn nhất của chatbot LLM là chúng chỉ mô phỏng ngôn ngữ mà không có khả năng hiểu sâu sắc và phản ánh thực tế. Nếu cần, có thể tạo một system message trước khi cắt để hướng dẫn hành vi của mô hình một cách cụ thể.

---

## Danh Sách Kiểm Tra Nộp Bài

- [ ] `python grade.py` — xem điểm tự động, mục tiêu ≥ 75/100
- [ ] Cả 4 checkpoint pytest đều pass
- [ ] Tất cả 9 câu trong file này đã được trả lời
- [ ] Đã copy bài làm vào folder `solution/`, push lên fork và dán link trên trang bài Lab ở VLearn trước 23:59 ngày 11/09/2026
