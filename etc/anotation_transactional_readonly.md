# @Transactional(readonly)

## @Transactional 주석이란?

- Spring 애플리케이션에서 트랜잭션 동작을 관리하는 핵심 요소.
- 데이터베이스 작업을 위한 안전망이며, 오류가 있는 경우 데이터 변경이 완전하고 안전하게 수행되거나 전혀 수행되지 않도록 보장한다.
- 이 경우 데이터를 망칠 수 있는 부분 업데이트나 변경을 방지하는데 도움이 된다.
- 그중에서... (readonly = true 혹은 readonly = false)에 대하여...

---

### # @Transactional(readonly = true)

- @Transactional(readOnly = true)는 데이터를 읽는 데만 사용되는 트랜잭션에 사용된다.
- 이 주석의 이점은 트랜잭션을 읽기 전용으로 표시하면 성능 최적화가 가능해진다.
- 서비스 메소드에서 SQL의 SELECT 쿼리 데이터를 가져오는 작업에 주로 사용되는데 회원의 조회 서비스 클래스를 작성하여 클래스 상단에 작성한 경우다.

```java
@Service
@Transactional(readOnly = true)
public class CustomerQueryServiceImpl implements CustomerQueryService {

    private final CustomerRepository customerRepository;

    public CustomerQueryServiceImpl(CustomerRepository customerRepository) {
        this.customerRepository = customerRepository;
    }

    @Override
    public CustomerDto getCustomer(Long customerId) {

        Optional<Customer> result = customerRepository.findById(customerId);

        if(result.isPresent()) {
            return new CustomerDto(result.get());
        }

        throw new RuntimeException("not found customer");
    }
}
```

---

### # @Transactional(readonly = false)

- @Transactional(readOnly = false)는 @Transactional의 기본설정으로 데이터를 읽는 것뿐만 아니라 수정하는 작업(삽입, 업데이트, 삭제)을 포함할 때 사용한다.
- 이 주석은 트랜잭션이 데이터를 변경할 수 있기 때문에, 데이터베이스 시스템은 데이터 무결성과 일관성을 보장해야 한다.
- 데이터베이스의 상태를 변경하는 메소드에 이 설정이 필수적이다. 레코드를 업데이트하거나, 새로운 데이터를 삽입하는데 이 설정을 사용하는데 회원의 정보를 기존 레코드와 입력받은 레코드의 메소드가 종료 시점을 비교하며 변경을 시도하는 경우다.

```java
@Transactional
@Override
public void updateCustomer(Long customerId, InputCustomerRequest request) {

    Customer customer = customerRepository.findById(customerId).orElseThrow(NotFoundCustomerException::new);

    customer.update(request);
}
```
