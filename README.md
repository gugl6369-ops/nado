# nado
@mixin leaner-border{
  position: relative;
  justify-content: center;
  align-items: center;

  &::before{
    content: '';
    width: 100%;
    height: calc(100% + 2px);
    position: absolute;
    border-radius: 38px;
    background: linear-gradient(90deg, transparent, #424242, rgba(66, 66, 66, 0.51), transparent);
    z-index: -1;
  }
}
