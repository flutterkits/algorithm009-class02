class Solution {
    public List<List<Integer>> levelOrder(Node root) {
       List<List<Integer>> result = new ArrayList<>();
       if(root!=null){
            List<Node> roots = new ArrayList<>();
            roots.add(root);
            findNodes(roots,result);
       }
        return result;
    }

    private void findNodes(List<Node> nodes,List<List<Integer>> result){
        if(nodes !=null && nodes.size()>0){
            List<Node> children = new ArrayList<>();
            List<Integer> nodesVal = new ArrayList<>();
            for(Node node:nodes){
                if(node.children!=null && node.children.size()>0){
                    children.addAll(node.children);
                }
                nodesVal.add(node.val);
            }
            result.add(nodesVal);
            if(children.size()>0){
                findNodes(children,result);
            }
            
        }   
    }
}