# mdl-et718-20220428-rails-hr-repo

rails generate model Article title:string text:text
rails generate scaffold Resume name image_url role location email phone




rails generate model Comment commenter:string body:text article:references
rails generate model Skill title level resume:references  




resources :articles do
  resources :comments
end

resources :resumes do
  resources :skills
end




rails generate controller Comments
rails generate controller Skills




class CommentsController < ApplicationController
  def create
    @article = Article.find(params[:article_id])
    @comment = @article.comments.create(comment_params)
    redirect_to article_path(@article)
  end
 
  private
    def comment_params
      params.require(:comment).permit(:commenter, :body)
    end
end

class SkillsController < ApplicationController
  def create
    @resume = Resume.find(params[:resume_id])
    @skill = @resume.skills.create(skill_params)
    redirect_to resume_path(@resume)
  end
 
  private
    def skill_params
      params.require(:skill).permit(:title, :level)
    end
end




<p>
  <strong>Commenter:</strong>
  <%= comment.commenter %>
</p>
 
<p>
  <strong>Comment:</strong>
  <%= comment.body %>
</p>
************************************************
<p>
  <strong>Title:</strong>
  <%= skill.title %>
</p>
 
<p>
  <strong>Level:</strong>
  <%= skill.level %>
</p>



<%= form_for([@article, @article.comments.build]) do |f| %>
  <p>
    <%= f.label :commenter %><br>
    <%= f.text_field :commenter %>
  </p>
  <p>
    <%= f.label :body %><br>
    <%= f.text_area :body %>
  </p>
  <p>
    <%= f.submit %>
  </p>
<% end %>
*****************************************************

<%= form_for([@resume, @resume.skills.build]) do |f| %>
  <p>
    <%= f.label :title %><br>
    <%= f.text_field :title %>
  </p>
  <p>
    <%= f.label :level %><br>
    <%= f.text_field :level %>
  </p>
  <p>
    <%= f.submit %>
  </p>
<% end %>






<p>
  <%= link_to 'Destroy Comment', [comment.article, comment],
               method: :delete,
               data: { confirm: 'Are you sure?' } %>
</p>
*************************************************************
<p>
  <%= link_to 'Remove Skill', [skill.resume, skill],
               method: :delete,
               data: { confirm: 'Are you sure?' } %>
</p>









 def destroy
    @article = Article.find(params[:article_id])
    @comment = @article.comments.find(params[:id])
    @comment.destroy
    redirect_to article_path(@article)
  end
  *****************************************************
   def destroy
    @resume = Resume.find(params[:resume_id])
    @skill = @resume.skills.find(params[:id])
    @skill.destroy
    redirect_to resume_path(@resume)
  end
  
  
  
  
  
<h2>Comments</h2>
<%= render @article.comments %>
 
<h2>Add a comment:</h2>
<%= render 'comments/form' %>
****************************************
<h2>Skills</h2>
<%= render @resume.skills %>
 
<h2>Add a skill:</h2>
<%= render 'skills/form' %>
  
  
  
  
  
  
  