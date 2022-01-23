# typeorm

## Many-to-one / one-to-many relations

```typescript
import {Entity, PrimaryGeneratedColumn, Column, ManyToOne} from "typeorm";
import {User} from "./User";

@Entity()
export class Post {

    @PrimaryGeneratedColumn()
    id: number;

    @Column()
    url: string;

    @Column()
    author_id:number;

    @ManyToOne(() => User, user => user.posts)
    @JoinColumn({ name: 'author_id' })
    author: User;

}
```

```typescript
import {Entity, PrimaryGeneratedColumn, Column, OneToMany} from "typeorm";
import {Post} from "./Post";

@Entity()
export class User {

    @PrimaryGeneratedColumn()
    id: number;

    @Column()
    name: string;

    @OneToMany(() => Post, post => post.author)
    posts: Post[];

}
```

- `@ManyToOne`만 필요할 경우 `@OneToMany`가 없어도 된다.
- 하지만, `@OneToMany`를 사용해야 하는 경우 `@ManyToOne`은 반드시 존재해야 한다.

```typescript
const userRepository = connection.getRepository(User);
const users = await userRepository.find({ relations: ["posts"] });

// or from inverse side

const photoRepository = connection.getRepository(Post);
const posts = await photoRepository.find({ relations: ["author"] });
```

- `FindOptions`에 `relations`를 지정하여 로드할 수 있다.


### references

- [Many-to-one / one-to-many relations - typeorm](https://orkhan.gitbook.io/typeorm/docs/many-to-one-one-to-many-relations)