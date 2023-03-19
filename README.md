# Random_Code_Snippets

## 1 Password Encoder

        @Autowired
      private UserInfoRepository repository;

      @Autowired
      private PasswordEncoder passwordEncoder;


      public String addUser(UserInfo userInfo) {
        userInfo.setPassword(passwordEncoder.encode(userInfo.getPassword()));
        repository.save(userInfo);
        return "user added to system ";
       }
       
       
       
       
## 2  Stream to find the id ,in list of products
 
        public Product getProduct(int id) {
        return productList.stream()
                .filter(product -> product.getProductId() == id)
                .findAny()
                .orElseThrow(() -> new RuntimeException("product " + id + " not found"));
        }


## 3 Headers in RestAPI

        @GetMapping("/downloads/{filename}")
	public ResponseEntity<Resource> downloadFile(@PathVariable("filename") String filename) throws IOException {
		//		ClassPathResource file = new ClassPathResource(filename + ".txt");


		//		System.out.println(file.getFilename() + " " + file.getPath());
		org.springframework.http.HttpHeaders headers = new org.springframework.http.HttpHeaders();
		headers.add(org.springframework.http.HttpHeaders.CONTENT_DISPOSITION,
				"attachment; filename=" +filename );
		headers.add("Cache-Control", "no-cache, no-store, must-revalidate");
		headers.add("Pragma", "no-cache");
		headers.add("Expires", "0");

		
		FileInputStream fileInputStream = new FileInputStream("fileD.txt");
		byte [] data = new byte[fileInputStream.available()];

		InputStream inputStream = new ByteArrayInputStream(data);
		Resource resource = new InputStreamResource(inputStream);


		Scanner scanner = new Scanner(fileInputStream);

		while(scanner.hasNext())
		{
			String nextLine = scanner.nextLine();
			System.out.print(nextLine);
		}
		return new  ResponseEntity<>(resource,headers, HttpStatus.OK );
	      }
