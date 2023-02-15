# 유저 서비스의 인터페이스

| 기능 | 엔드포인트 | 본문 데이터 예(JSON) | 쿼리 파라미터 | 패스 파라미터 | 응답 |
|:--------|:----------:|----------:|:----:|:---------:|:-----------:|
| 회원가입 | POST/users |{"name":"Dexter","email":"dexter.haan@gmail.com","password": "PASSWORD"} | | |201|
| 이메일 인증 | POST/users/email-verify | {"signupVerifyToken":"임의의문자열"} || | 201 엑세스 토큰 |
| 로그인 | POST/users/login | {"email":"dexter.hann@gmail.com","password":"PASSWORD"} || | 201 엑세스 토큰 |
| 회원 정보 조회 | GET/users/:id |  | | id:유저 생성시 만들어진 유저 ID,email이 아니라 임의의 문자열 | 200 회원정보 |
> AppController, AppService 삭제

#### app.module.ts
```
import { Module } from '@nestjs/common';
import { UserController } from './users/users.controller';

@Module({
  imports: [],
  controllers: [UserController],
})
export class AppModule {}
```
#### userController
```
import { Body, Controller, Get, Param, Post, Query } from '@nestjs/common';
import { CreateUserDto, UserLoginDto, VertifyEmailDto } from './dto/create-user.dto';
import { UserInfo } from './UserInfo';

@Controller('users')
export class UserController {
  @Post()
  async createUser(@Body() dto: CreateUserDto): Promise<void> {
    console.log(dto);
  }
  @Post('/email-verify')
  async vertifyEmail(@Query() dto: VertifyEmailDto): Promise<string> {
    console.log(dto);
    return;
  }
  @Post('/login')
  async login(@Body() dto: UserLoginDto): Promise<string> {
    console.log(dto);
    return;
  }
  @Get('/:id')
  async getUserInfo(@Param('id') userId: string): Promise<UserInfo> {
    console.log(userId);
    return;
  }
}
```
#### CreateUserDto
```
export class CreateUserDto {
  readonly name: string;
  readonly email: string;
  readonly password: string;
}
export class VertifyEmailDto {
  signupVerifyToken: string;
}
export class UserLoginDto {
  email: string;
  password: string;
}
```
#### Talend API Tester(Chrom 확장프로그램)
![](https://velog.velcdn.com/images/chch4lee1/post/41d8d514-67e3-4595-9f8f-b52f4187b28c/image.png)
![](https://velog.velcdn.com/images/chch4lee1/post/0d999681-e08d-43fe-bdc8-563fc765f4ea/image.png)
![](https://velog.velcdn.com/images/chch4lee1/post/2c62c171-b406-4748-a3cc-c248fc721e25/image.png)
![](https://velog.velcdn.com/images/chch4lee1/post/054c875c-53a4-4529-988f-956ee5bce70e/image.png)
#### 결과는 직접 확인






### 참고자료
https://wikidocs.net/158475
