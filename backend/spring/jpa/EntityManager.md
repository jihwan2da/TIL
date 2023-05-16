# EntityManager

- 트랜잭션 안에서 Entity를 관리하는 역할을 수행한다.  
- 영속성 컨텍스트를 통해서 Entity를 관리한다.  
- EntityManager를 통해서 수행되는 모든 작업은 트랜잭션 안에서 작업되어야 한다.    
- 쓰레드 안전하지 않아 쓰레드 간 공유하면 안된다.(사용 후 버려야 된다.)   

```java
    public void service() {
        EntityManager em = emf.createEntityManager();
        EntityTransaction tx = em.getTransaction();

        try {
            // EntityManager를 통해서 수행되는 모든 작업은 트랜잭션 안에서 작업되어야 한다.
            tx.begin();

            //Entity 영속화 처리 등등
            em.persist();

            //로직 성공 시 커밋
            tx.commit();
        } catch (Exception e) {
            //에러 시 롤백
            tx.rollback();
        } finally {
            // 다 쓴 EntityManager는 버려야한다. (Thread-Safe 하지 않아 다 썻으면 버려야한다.)
            // 또한 DB Connetion을 가지고 있기 때문에 버려야한다.
            em.close();
        }
    }
```

### Spring의 EntityManager 동시성 문제 해결  
- 쓰레드 간 안전하게 공유하기 위해 스레드로부터 EntityManager를 독립적으로 사용하도록 지원한다.
   - EntityManagerFactory를 빈으로 등록하여 애플리케이션 컨텍스트에서 공유한다.
   - 스레드마다 EntityManagerFactory에서 EntityManager를 하나 씩 부여받아 사용한다.
   - 사용을 마친 EntityManager를 닫는다.  
  

  위의 방법으로 EntityManager의 동시성 문제를 해결할 수 있다. 


