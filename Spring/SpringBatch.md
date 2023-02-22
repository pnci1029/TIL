## Back Process
#### Batch Job
  - 배치처리를 위한 전체작업
  - Job은 하나이상의 Step으로 구성
  - JobBuilder를 사용하여 생성
#### Batch Step
  - Job의 일부분, 단일작업형태
  - StepBuilder를 사용하여 생성
### JobBuilder와 StepBuilder 생성
```
@Configuration
@EnableBatchProcessing
public class BatchConfiguration {
 
    @Autowired
    public JobBuilderFactory jobBuilderFactory;
 
    @Autowired
    public StepBuilderFactory stepBuilderFactory;
 
    @Bean
    public Step step1() {                             ->step 생성 메소드
        return stepBuilderFactory.get("step1")
                .<String, String>chunk(10)            -> chunk() ->메소드를 활용하여 한번에 읽을 항목 수 설정
                .reader(reader())
                .processor(processor())
                .writer(writer())
                .build();
    }
 
    @Bean
    public Job job() {                              ->job 생성 메소드
        return jobBuilderFactory.get("job")
                .incrementer(new RunIdIncrementer())
                .start(step1())
                .build();
    }
    
    // Step에서 사용될 ItemReader, ItemProcessor, ItemWriter를 생성하는 코드
    // ...
}
```
#  
#  
## 배치 작업 실행
```
@SpringBootApplication
public class BatchApplication implements CommandLineRunner {

    @Autowired
    JobLauncher jobLauncher;

    @Autowired
    Job job;

    public static void main(String[] args) {
        SpringApplication.run(BatchApplication.class, args);
    }

    @Override
    public void run(String... args) throws Exception {
        JobParameters jobParameters

```
  - CommandLineRunner나 ApplicationRunner 인터페이스를 구현하는 클래스를 작성
  - JobLauncher 주입 후 Job 실행
