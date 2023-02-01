# Crawling_Product_Data_From_Tiki
Tiki là một trong những trang thương mại điện tử lớn nhất hiện nay. Những thông tin về sản phẩm, người bán và loại sản phẩm là một trong những thông tin vô cùng hữu ích cho các bạn học tập và phân tích. Với Project này, mình sẽ hỗ trợ các bạn cào thông tin sản phẩm từ trang chủ của của Tiki một cách rất trực quan. Cuối cùng, mình sẽ liên tục vừa cào và đẩy dữ liệu vào MySQL database

Cách xử lý việc liên tục cào và thêm dữ liệu:
![alt text](https://github.com/[username]/[reponame]/blob/[branch]/image.jpg?raw=true)

Main Thread: Chứa danh sách các categories_id và product_id để chia sẻ tài nguyên giữa các thread
    -> Khi mà đã cào hết data từ categories_id list thì việc cào dữ liệu sẽ ngừng lại
Product_id Thread: Khi thread này được chạy thì nó sẽ lấy categories_id đầu tiên để cào ra các product_id và thêm vào product_id  list ở Main thread

Product Data Thread:
    Task1: từ các product_id thì task này sẽ cào ra các dữ liệu về sản phẩm đó và phân bố vào 3 dataframe: product, categories và seller.
    Task2: từ các dataframe ta sẽ thêm dữ liệu này vào trong MySQL. Vì thread này tác động trực tiếp lên dataframe và sẽ xóa đi row của dataframe được thêm vào MySQL nên ta sẽ khóa thread ở task này để tránh gây ảnh hưởng tới dataframe trong quá trình chạy