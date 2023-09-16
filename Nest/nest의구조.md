## Nest의 기본 구조

Main.ts의 AppModule => AppMoudle에서 controller가 존재하고 => controller를 따라 return받은 service.ts의 비즈니스 로직을 수행한다.  
<br>
이 구조는 클라이언트가 해당되는 라우터에 들어가서 response를 받을 수 있도록 도와준다.

## Nest.js의 package.json과 Dependecies

nestjs/common,nestjs/core,@nestjs/platform-express : Nest안에서 자체적으로 동작하는 라이브러리

reflect-metadata: 데코레이터를 사용할 수 있게 도와주는 라이브러리

rxjs: 비동기 및 이벤트관련 코드 작성을 위한 라이브러리

<hr>

## Controller

컨트롤러는 애플리케이션에 대한 특청 요청을 수신하는 것.
데코레이터에서 경로 접두사를 사용하면 Routeing시에 특정 경로(예:@Get('/cats'))에 대한 라우팅을 선언하고 관리할 수 있다.

-Request 객체 관리
express에서 (req,res)를 받았던 것처럼 Nest에서도 @req()를 통해 Request객체에 접근할 수 있다.
express와 Nest의 코드를 비교해보자.

    router.get('/cats', (req, res) => {
        try {
            const cats = Cat;
            // throw new Error('db connect error');
            res.status(200).send({
            success: true,
            data: {
                cats,
            },
            });
        } catch (error) {
            res.status(400).send({
            success: false,
            error: error.message,
            });
        }
        });
    ```



    import { Controller, Get, Req } from '@nestjs/common';

    import { Request } from 'express';
    import { AppService } from './app.service';

    @Controller('cats')
    export class AppController {
        constructor(private readonly appService: AppService) {}

        @Get('hello')
        getHello(@Req() req: Request, @Body Body, @param param ): string {
        return this.appService.getHello();
        }
    }

또한 Request 객체의 body에 접근할때 express처럼 req.body로 접근하지 않아도 되고 해당 class의 Method의 argument에서 바로 접근할 수 있다. Request 객체의 Params도 마찬가지.

## Provider

<hr>
Nest의 기본 시스템은 모듈이다.

Nest의 공식문서를 참고하면 **많은 기본 Nest 클래스는 서비스, 리포지토리, 팩토리, 헬퍼 등 공급자로 취급될 수 있습니다.**라고 되어있다. 위에 작성한 코드를 보면 controller를 통해 service로 접근하는데 여기서 service가 provider로 취급되는것이다.

@Injectable()데코레이터를 통해 provider로 취급되어 dependency injection이 가능하다.

app.module.ts에 등록한 provider를 통해 controller는 provider를 인스턴스로 제공받아서 사용할 수 있다.

이것이 Nest의 의존성 주입이다.

## 캡슐화(은닉화)

모듈은 provider를 캡슐화한다. Nest에서는 기본적으로 exports되지 않은 모듈을 바깥에서 사용할 수 없다. 공급자가 현재 모듈의 일부분이 아니거나 exports를 하지 않은 공급자라면 provider를 사용할 수 없다.

exports를 하면 다른 모듈에서도 provider를 사용할 수 있다.(캡슐화 해제)

또한 **단일 책임의 원칙**을 준수하여 분리된 모듈을 최대한 격리한다.
