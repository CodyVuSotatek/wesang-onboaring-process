# 1. Ticket status:

Which status you can change:

- `in development`: start coding a ticket
- `code review`: submit code to get review
- `in approver check`: after ticket has been reviewed and approved (1 of Korean team and 1 of Sota team) and merging
- `ready for qa`: after your code is merged and deployed on staging server, you checked and it works

# 2. Ticket label:

- `DOWANT`: after this ticket is approved and waiting for deploying on staging. You must set it
- `hold deploy`: wait a related ticket to be done/merge together with this ticket, or it will be over limit times of deploy in day (2
  times per day)

# 3. Git flow

## 3.1. Check out from master (for every ticket)<br/>

- Change ticket status to: `in development`
- Some rules:<br/>
    - Branch name start with lower ticket id (example: mrt-357)
    - Check out from master only
    - Valid character is `a-z0-9` and `-`
      <br/>**Example:**

    ```bash
    git checkout -b mrt-357-something-to-do origin/master
    ```

## 3.2. If any ticket is done (merged on staging) and you need code from this ticket, Let's merge it<br>

**Example**:

   ```bash
    git merge origin/mrt-356-something-here
   ```

## 3.3. Do your change on this branch

Some rules:

- use `''` instead of `""` for string
- try to use constant instead of string
- PEP8 format
- follow team convention
- Commit format: [Ticket_id] type: message<br>
  **Example:** `MRT-357 Feat: create api to get restaurant campaign`

## 3.4. Creating PR to code-review

- Change ticket status to `code review`
- Add reviewer: A Korean team ( for example @Mr. Lee ChangWoo) and a Sotatek team member
- Add pull request detail follow this template:
  ```
    [ Commit Message ]
    1. 41c6ad1
    모듈화 해서 관리하기 위해 SubscriptionPayRequest 가 공짜의 금액인지 is_free 랑 취소 및 환불했을 경우 사용할 cancel 인스턴스 메서드를 생성

    2. 8e5905d
    이니시스 환불 오류건 수정

    3. f864c32
    카카오결제 환불 오류건 수정
  ```
  You can see it [here](https://github.com/yogiyo/Yogiyo_Web/pull/16288)

## 3.5. If there are any issues in this PR:

- Add commit link in
  reply [issuecomment-1519356676](https://github.com/yogiyo/Yogiyo_Web/pull/16277#issuecomment-1519356676)
- Make sure pass all CI on GitHub
- You can ignore `security findings` label is tagged by github-actions

## 3.6. When you have 2 approves (includes Mr.Lee and Sotatek team)

- Ticket status will be automatically changed to `In approver check`

## 3.7. Merge your ticket

- Notify Ms.Lee that you will merge it
- If having conflict:
    + Checkout newest code-review on local

```bash
git checkout master
git branch -D code-review
git fetch -p
git checkout code-review
```

+ Merge your branch on origin

```bash
git merge origin/mrt-357-something-to-do
```

+ Resolve conflict on your local
+ Take note resolve conflict action (it will help Mr.Lee to resolve this conflict on other branches)
+ If you don't know how to resolve a conflict, please communicate with author of this commit
+ Run testcase again
+ Notify Mr.Lee that you are going to push your code-review
+ Push your local code-review to origin

```bash
git push origin code-review
```

+ Notify Mr.Lee and tell him how to you resolve conflict (use your note is one way)
+ Put label `dowant` to this ticket

## 3.8. Deploy on staging server

+ After you merge your PR, please notify Mr.Lee and he will deploy it on c/e-staging
+ After this deploy is done, let check your code on staging
+ Note to this ticket (print Postman screen or something else)
+ Notify Mr.Lee
+ Update ticket status to `Ready for QA`

## 3.9. When you find any issues and fix there on your branch. Please start from step 4
