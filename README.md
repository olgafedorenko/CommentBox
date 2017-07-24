# CommentBox
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>Share your mind</title>
    <link rel="stylesheet" href="com.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.13.3/react.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.13.3/JSXTransformer.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.1/jquery.min.js"></script>
    <script src="https://fb.me/react-15.2.0.js"></script>
    <script src="https://fb.me/react-dom-15.2.0.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.23/browser.min.js"></script> 
    <script src="http://cdnjs.cloudflare.com/ajax/libs/showdown/0.3.1/showdown.min.js"></script>
</head>
    <body>
        <img src="picture.jpeg" alt="talk" id="pictureTalk">
        <h1 id="meaning">Meaning Of Life Quotes</h1>
        <div id="app"></div>
        <script type="text/babel">
         var Comment = React.createClass({
             getInitialState: function() {
             return {editing:false}
             
         },
            edit: function(){
             this.setState({editing:true})
         },
             remove:function(){
                this.props.deleteFromBoard(this.props.index)
                 
             },
             save: function(){
                 // referenve to new Text what types
                this.props.updateCommentText(this.refs.newText.value, this.props.index)
                 this.setState({editing:false})
         },
             renderForm: function(){
                return (
                     <div className="commentContainer">
                         <textarea ref="newText" className="textareaContainer" defaultValue={this.props.children}></textarea>
                             <button onClick={this.save} className="save">Save</button>      
                    </div>
                 
             )},
             renderNormal: function(){
                 return(
                    <div className="commentContainer">
                         <div className="commentText"> <p>{this.props.children}</p> </div>
                         <button onClick={this.edit} className="edit">Edit</button>
                         <button onClick={this.remove} className="remove">Remove</button>
                         <hr /> 
                    </div>
                     
             )
             },
             render:function () {
                 if(this.state.editing){
                        return this.renderForm();
                    }
                 else{
                        return this.renderNormal();
                    }
             }
         
})
         
         var Layout= React.createClass({
            getInitialState: function(){
               return{
                   comments:[
                       "“You will never be happy if you continue to search for what happiness consists of. You will never live if you are looking for the meaning of life.”",
                       "“Life has to be given a meaning because of the obvious fact that it has no meaning.” "
                   ]
               } 
            },
             addComment(){
                 var val=this.refs.name.value
                 var arr=this.state.comments;
                    arr.push(val)
                    this.setState({comments:arr})
                  this.refs.name.value=''
                 
             },
            
             updateComment(newText,i){
                 var arr = this.state.comments
                 arr[i]=newText
                 this.setState({comments:arr})
                 
             },
             removeComment(i){
                 var arr=this.state.comments;
                 arr.splice(i,1)
                 this.setState({comments:arr})
                 
             },
             eachComment: function(text,i){
                 return (
                     <Comment key={i} index={i} updateCommentText={this.updateComment} deleteFromBoard={this.removeComment}>{text}
                     </Comment>
                 )
             },
             handleKeyPress(target) {
    if(target.charCode==13){
            this.addComment()  
        this.refs.name.value=''
        
    }
                 
},
             render(){
                 return(
                     
                     <div>
                         <div>
                            {this.state.comments.map(this.eachComment)}
                         </div>
                         <div className="addNew">
                         <textarea className="textareaContainer" type="text" ref="name"  placeholder="Type your mind" onKeyPress={this.handleKeyPress}/>
                         <button type="submit" className="add" onClick={this.addComment.bind(null, this)}>Add new</button>
                             
                            </div>
                         
                         
                    </div>
            
             )}
         })
ReactDOM.render(<Layout/>,document.getElementById('app'))
        
        </script>
    </body>
</html>
