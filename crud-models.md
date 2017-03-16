[CRUD]Post, Comment
===========

# 1. 게시글
## 1-1. 아웃라인 만들기
    1. post 컨트롤러를 먼저 만들고 index 파일과 new을 만든다.
    2. 컨트롤러에서 뷰파일과 동일한 액션을 만들어준다(def index..).
    3. index.html.erb에 메인 페이지를 넣고 new.html.erb에 입력 폼(user, title, content)을 만든다.
      * index.html.erb
        <h1>게시판</h1>

        <ul>
          <li>이름: </li>
          <li>제목: </li>
          <li>내용: </li>
        </ul>
      * new.html.erb
        <form action="/create" method="POST">
          <label for="user">이름</label>
          <input type="text" name="user" placeholder="이름을 입력해주세요"><br />
          <label for="title">제목</label>
          <input type="text" name="title" placeholder="제목을 입력해주세요"><br />
          <label for="content">내용</label>
          <input type="text" name="content" placeholder="내용을 입력해주세요"><br />
          <button>작성완료</button>
        </form>


## 1-2. create 액션 만들기
    1. post 컨트롤러에 들어가서 create 액션을 만들어준다.
    2. create.html.erb도 만들어준다. '생성되었습니다' 정도 뜨게.
    3. new.html.erb의 폼과 create 액션을 연결한다.
      * routes에 경로잡기
        root 'posts#index'
        get '/index' => 'posts#index'
        get '/new' => 'posts#new'
        post '/create' => 'posts#create'

      # 에러
        `ActionController::InvalidAuthenticityToken in PostsController#create
        ActionController::InvalidAuthenticityToken`
        이런 에러 뜨면 controllers 폴더에 들어가서 application_controller.rb

    4. 잘 받아와지는지 확인하려면 create.html.erb에 뜨도록 해본다(model에 들어가야 id가 자동으로 부여되서 id로는 안찾아짐).
      * posts_controller.rb
        `@username = params[:user]
        @title = params[:title]
        @content = params[:content]`
      * create.html.erb
        `<p><%= @username %></p>
        <p><%= @title %></p>
        <p><%= @content %></p>`


## 1-3. model에 저장하기
    1. form과 create가 잘 연결되었다면 모델(Post user:string title:string content:text)을 만든다.
      $ rails g model post user:string title:string content:text
      $ rake db:migrate
    2. create 액션에서 받아온 정보를 model에 저장한다.
      * create 액션에 작성
        post = Post.new
        post.user = params[:user]
        post.title = params[:title]
        post.content = params[:content]
        post.save!
    3. 모델에 저장이 잘되고있는지 콘솔창을 통해 확인하고, index에 정보를 나타내도록한다.
      * index 액션
        @posts = Post.all
      * index.html.erb
        <% @posts.each do |post|%>
        <ul>
          <li>이름: <%= post.user %></li>
          <li>제목: <%= post.title %></li>
          <li>내용: <%= post.content %></li>
        </ul>
        <% end %>
    4. 잘 되는거 확인했으면 create 뷰파일은 지우고 redirect_to를 추가한다.
      * redirect_to
        redirect_to '/index'
      # redirect_to 뒤에 들어가는 경로는 반드시 routes에 쓴 경로대로 쓴다. 아니면 에러남. 만약, routes에 posts/index라고 설정했다면 반드시 앞에 posts를 붙여야한다.
      # routes랑 mode은 수정하고나면 서버 재시작!

#2. 댓글
##2-1.
##2-2.
##2-3.
##2-4.
