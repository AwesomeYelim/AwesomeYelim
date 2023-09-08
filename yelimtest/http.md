# wtf...304 status code 에 대해서

- local에서는 잘되었는데 vercel에 배포이후에 crud를 시도하면 firebase에서 get하는 과정에서 업데이트가 안된 데이터를 불러왔다..

> 원인은 바로 304 ...에러.. 아니 정확히는 status code라고 한다

- 거의 3일 가까이를 삽질했던거 같다.. 뭐 크롬 캐시를 지워라..header 의 Cache-Control을 no-store로 보내라 뭐 unique tag를 보내라 등등 다해보았던거 같다...

- 하지만 나는 내가 nextjs 로 짜논 서버의 전면적인 구조가 잘못되었다는 생각이 계속 들었당..

```ts
// service/posts.ts

export async function getPosts(): Promise<Post[]> {
  const fireposts = await getDocs(collection(db, "posts"));
  let posts: Post[] = [];

  fireposts.forEach((doc) => {
    posts.push(doc.data() as Post);
  });

  return posts;
}
```

- 여기서 firebase에서 공통으로 data를 가져오는 함수를 만든뒤

```ts
// app/api/route.ts

import { getPosts } from "@/service/posts";
import { NextResponse } from "next/server";

export async function GET(req: Request) {
  const posts = await getPosts();

  return NextResponse.json(posts);
}
```

- 여기서 api를 공통으로 가져올수 있도록..(어떻게 보면 우회해서 정보를 가지고 오고있던셈 ㅎ )

- 그냥 client 에서도 db 를 직박으로 가져올수 있다는 사실을 알면서 왜 저러고 있었을까..?.ㅎ 나중에 정리해야 겠다라는 생각으로 내비두고 있었던거 같다.ㅎ

- 그냥 서버를 따로 생성하지 말고 client 에서 직접 불러와주면 데이터를 가져올때마다 firebase 자체에서 유니크 쿼리를 보내준다.(304 따위는 생길리 없음 ~~~)

```ts
// components/common/functions/myapi.ts

export const getPostsApi = async () => {
  const fireposts = await getDocs(collection(db, "posts"));

  let posts: Post[] = [];

  fireposts.forEach((doc) => {
    posts.push(doc.data() as Post);
  });

  return posts ? posts : [];
};
```
