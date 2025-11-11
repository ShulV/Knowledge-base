## Сжать, обрезать изображение
#squash #compress #cut #truncate #crop #clip #squeeze
```java
@Transactional  
@Scheduled(fixedDelay = 10000)  
public void imageSquash() throws IOException {  
    Image image = jdbcClient.sql("""  
        SELECT id, date_add, bytes  
          FROM image  
      ORDER BY date_add DESC  
         LIMIT 1  
    """)  
            .query((rs, rowNum) -> {  
                return new Image(  
                        rs.getLong("id"),  
                        rs.getDate("date_add"),  
                        rs.getBytes("bytes")  
                );  
            })  
            .single();  
  
    try (InputStream inputFile = new ByteArrayInputStream(image.bytes());  
         ByteArrayOutputStream outputStream = new ByteArrayOutputStream()) {  
  
        Thumbnails.of(inputFile)  
                .size(1200, 800)  
                .outputFormat("jpg")  
                .outputQuality(0.7)  
                .toOutputStream(outputStream);  
  
        byte[] squashedBytes = outputStream.toByteArray();  
  
        jdbcClient.sql("INSERT INTO image (bytes) VALUES (:bytes)")  
                .param("bytes", squashedBytes)  
                .update();  
    }  
}
```