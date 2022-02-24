CALL gds.alpha.closeness.stream({
  nodeProjection: 'FIGHTERS',
  relationshipProjection: 'FIGHT_AGAINST'
})
YIELD nodeId, centrality
RETURN gds.util.asNode(nodeId).name AS user, centrality
ORDER BY centrality DESC