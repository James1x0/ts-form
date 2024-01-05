# TS Form
👋 TS Form is a project for people who hate making forms. We use [MDX](https://mdxjs.com/) to transit generated form definitions from backends to frontends.

> There are literally thousands of form libraries out there, but all of them share the same problems. They are one or many of the following:

➡️ 🕸 Outdated or abandoned

➡️ 🎛 Complicated

➡️ 📚 Require reading significant documentation to set up

➡️ 👎 Suck


## ⚡️ TS Form aims to be the "go-to" "plug n' play" solution for forms if you're using a supported ORM, Typescript, & React.

> 🪄 Let me show you how easy it is in three steps.

## 1️⃣
> Define a form in your entity:

```ts
// ./entities/Animal.ts

import { Column, Entity } from 'typeorm';
import { TsForm } from 'ts-form/typeorm';

@TsForm() // ⬅️ Here it is! The Magic 🪄
@Entity()
export class Animal {
  @Column({ unique: true }) name: string;

  @Column() traitsHappy: Boolean;
  @Column() traitsFuzzy: Boolean;
  @Column() traitsTailType: String;

  @Column({
    type:    'enum',
    enum:    Color,
  }) color: Color; // An enumerable!
}
```

## 2️⃣

> Wire up an API for it:

```ts
// Anywhere you define api routes

import { getForm } from 'ts-form';

api.get('/api/forms/:entity', (request: FastifyRequest, reply: FastifyReply) => {
  const { entity } = request.params;
  const form = await getForm(entity); // ⬅️ One liner to get form MDX
  reply.status(200).send({ form });
}
```

## 3️⃣

> Then, plug it into your React frontend:

```jsx
import { useTsForm, Field, Title, Grid, FormType } from 'ts-form/react';

function CreateAnimalPage (props) {
  const [ TsForm ] = useTsForm({
    entity: 'Animal',
    type: FormType.Create,
    // Use our components for rendering the form, or roll your own for customizability!
    formComponents: {
      Field,
      Title,
      Grid
    }
  });

  return (
    <section>
      <h1>Create an animal!</h1>
      <TsForm
        onSave={(data) => {
          /*
            Do something with the data.
            It's actually safe to send this directly to your API!
          */
        }}
      />
    </section>
  );
}
```

### 🎉 Viola! A Wild Form Appears!

![](https://github.com/James1x0/ts-form/blob/main/example.png?raw=true)

