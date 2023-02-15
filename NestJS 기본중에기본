# src 내부파일
#### app.controller.ts : 하나의 경로를 가진 기본 컨트롤러
#### app.controller.spec.ts : 컨트롤러에 대한 유닛 테스트
#### app.module.ts : Nest 어플리케이션의 루트 모듈(모든 Nest모듈은 여기서 연결되어야함)
#### app.service.ts : 하나의 메소드를 가진 기본 서비스
#### main.ts : Nest Appication의 엔트리 파일
# Controller
- @Controller()는 express의 app.use('/', router)에서 '/'와 같은 역할
- @Controller('say') 이렇게 인자로 string을 넘겨주면 express에서 app.use('/say',router)와 같은 코드
### 상태코드
```typescript
@Post()
@HttpCode(204)
create() {
  return 'This action adds a new cat';
}
```
- 응답 상태코드는 201인 POST요청을 제외하고 기본적으로 항상 200입니다
- **@HTTPCode(...)**데코레이터를 추가하여 동작을 쉽게 변경 가능
### 헤더
```typescript
@Post()
@Header('Cache-Control', 'none')
create() {
  return 'This action adds a new cat';
}
```
- 사용자 지정 응받 헤드를 지정하려면 **@Header()** 데코레이트 혹은 라이브러리 특정 응답 객체를 사용 가능
- ex) **res.header()**
### 리디렉션
```typescript
@Get()
@Redirect('https://nestjs.com', 301)
```
- 응답을 특정 URL로 리디렉션하려면 @Redirect()데코레이터 또는 라이브러리 특정 응답 객체를 사용함
- ex) **res.redirect()**
- **@Redirect()**는 2개의 인수를 받음(url,statusCode)
- 모두 필수는 아님
### 경로 매개변수
> 요청의 일부로 동적인 데이터를 받아야 할 경우

- 매개변수가 있는 경로를 사용하기 위해서는 경로에 매개 변수 토큰을 추가하여 요청 URL의 해당 위치에서 동적 값을 잡아낼 수 있음
```typescript
@Get(':id')
findOne(@Param() params): string {
  console.log(params.id);
  return `This action returns a #${params.id} cat`;
}
```
- **@Param()** 데코레이터는 경로 매개 변수에 접근할때 사용함
- 경로 매개변수 id를 참조할 수 있음
### 하위 도메인 라우팅
```typescript
@Controller({ host: 'admin.example.com' })
export class AdminController {
  @Get()
  index(): string {
    return 'Admin page';
  }
}
```
- **@Controller** 데코레이터는 host 옵션을 사용하여 들어오는 요청의 HTTP호스트가 특정 갑과 일치해야지 처리하는 옵션을 추가할 수 있음
```typescript
@Controller({ host: ':account.example.com' })
export class AccountController {
  @Get()
  getInfo(@HostParam('account') account: string) {
    return account;
  }
}
```
- 경로 매개변수처름 host 옵션도 토큰을 사용하여 호스트 이름의 특정 위치에서 동적 값을 가져오기 가능
- 선언한 호스트 매개변수는 각 핸들러의 **@HostParam()** 데코레이터를 사용하여 접근 가능
### 비동기
> 데이터를 추출하는 과정은 대부분 비동기적
**async함수**를 통해 지원함

```typescript
@Get()
async findAll(): Promise<any[]> {
  return [];
}
```
- 모든 비동기 함수는 **Promise**를 반환해야함
### 요청 페이로드

# 수정중




#### 참고자료
https://velog.io/@ordidxzero/nestjs-basic-concept
https://www.wisewiredbooks.com/nestjs/overview/03-controller-2.html
