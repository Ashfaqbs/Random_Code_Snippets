# Random_Code_Snippets

## 1

        @Autowired
      private UserInfoRepository repository;

      @Autowired
      private PasswordEncoder passwordEncoder;


      public String addUser(UserInfo userInfo) {
        userInfo.setPassword(passwordEncoder.encode(userInfo.getPassword()));
        repository.save(userInfo);
        return "user added to system ";
       }
       
       
       
       
## 2 
 
        public Product getProduct(int id) {
        return productList.stream()
                .filter(product -> product.getProductId() == id)
                .findAny()
                .orElseThrow(() -> new RuntimeException("product " + id + " not found"));
        }
